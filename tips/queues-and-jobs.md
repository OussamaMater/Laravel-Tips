# Queues & Jobs Tips ([cd ..](../README.md))

- [Dispatch After Response](#laravel-tip--dispatch-after-response-️)
- [Delete a Job When Models Are Missing](#laravel-tip--delete-a-job-when-models-are-missing-️)
- [Clean Up After Failed Jobs](#laravel-tip--clean-up-after-failed-jobs-️)
- [Skip Relationships in Queues](#laravel-tip--skip-relationships-in-queues-️)
- [Bulk Dispatch](#laravel-tip--bulk-dispatch-️)
- [Skip Jobs When Batch is Cancelled](#laravel-tip--skip-jobs-when-batch-is-cancelled-️)
- [Skip Jobs](#laravel-tip--skip-jobs-️)
- [Keeping Jobs Unique Until Processing](#laravel-tip--keeping-jobs-unique-until-processing-️)
- [Rate Limit Jobs](#laravel-tip--rate-limit-jobs-️)
- [Monitor Failed Jobs](#laravel-tip--monitor-failed-jobs-️)
- [Fail Jobs on Specific Exceptions](#laravel-tip--fail-jobs-on-specific-exceptions-️)
- [Display Remaining Attempts for a Rate-Limited Job](#laravel-tip--display-remaining-attempts-for-a-rate-limited-job-️)
- [Encrypt Your Jobs](#laravel-tip--encrypt-your-jobs-️)
- [Global Middleware for Jobs](#laravel-tip--global-middleware-for-jobs-️)

## Laravel Tip 💡: Dispatch After Response ([⬆️](#queues--jobs-tips-cd-))

At times, certain tasks, like sending emails, don't necessarily need to be queued and processed by a worker. In such cases, you can make use of "dispatchAfterResponse()." True to its name, this method dispatches the job right after the server responds to the user. A quick response for the client without burdening the worker with minor tasks 🚀

```php
<?php

use App\Jobs\SendNotification;

SendNotification::dispatchAfterResponse();
```

## Laravel Tip 💡: Delete a Job When Models Are Missing ([⬆️](#queues--jobs-tips-cd-))

Eloquent models injected into jobs are auto-serialized for the queue and may trigger a `ModelNotFoundException` if deleted while waiting for a worker; you can quietly discard such jobs by setting `deleteWhenMissingModels` to true 🚀

```php
<?php

use Illuminate\Contracts\Queue\ShouldQueue;

class UpdateSearchIndex implements ShouldQueue
{
    /**
     * Delete the job if its models no longer exist.
     *
     * @var bool
     */
    public $deleteWhenMissingModels = true;
}
```

## Laravel Tip 💡: Clean Up After Failed Jobs ([⬆️](#queues--jobs-tips-cd-))

When jobs fail, you may want to send notifications or perform some cleanups. Luckily, Laravel allows you to define a "failed" method to do exactly that 🚀

```php
<?php

namespace App\Jobs;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Queue\SerializesModels;
use Throwable;

class ProcessPodcast implements ShouldQueue
{
    use InteractsWithQueue, Queueable, SerializesModels;

    // ...

    public function failed(?Throwable $exception): void
    {
        // Handle job failure, such as sending notifications
    }
}
```

## Laravel Tip 💡: Skip Relationships in Queues ([⬆️](#queues--jobs-tips-cd-))

When passing a model to a job, consider using the "WithoutRelations" attribute to skip serializing the relationships if you don't need them. This will keep the payload minimal and memory efficient 🚀

```php
<?php

use Illuminate\Queue\Attributes\WithoutRelations;

public function __construct(
    #[WithoutRelations]
    public Podcast $podcast
) {}
```

## Laravel Tip 💡: Bulk Dispatch ([⬆️](#queues--jobs-tips-cd-))

While Laravel offers batches to dispatch jobs, sometimes you just want to fire and forget. In that case, you can bulk dispatch instead of doing it one by one 🚀

```php
<?php

// If you are using the database driver, this will result in N queries
$users->each(fn(User $user) => GenerateInvoice::dispatch($user));

// This will result in a single query
$jobs = $users->map(fn(User $user) => new GenerateInvoice($user))->toArray();
Queue::bulk($jobs);
```

## Laravel Tip 💡: Skip Jobs When Batch is Cancelled ([⬆️](#queues--jobs-tips-cd-))

When working with batched jobs, it's best to check if the batch is canceled before running the job, and you don't have to do it manually because the "SkipIfBatchCancelled" middleware does exactly this 🚀

```php
<?php
use App\Jobs\ImportContacts;
use Illuminate\Support\Collection;

// A batched job
public function handle(): void
{
    if ($this->batch()->cancelled()) {
        return;
    }
}

public function middleware(): array
{
    return [new SkipIfBatchCancelled];
}
```

## Laravel Tip 💡: Skip Jobs ([⬆️](#queues--jobs-tips-cd-))

Ever needed to skip job execution? While you can do it manually, Laravel ships with a "Skip" middleware to do exactly that 🚀

```php
<?php

use Illuminate\Queue\Middleware\Skip;

public function middleware(): array
{
    return [
        Skip::when($someCondition),
        // You can also use `unless` and pass a closure
        Skip::unless(fn () => $this->shouldNotSkip()),
    ];
}
```

## Laravel Tip 💡: Keeping Jobs Unique Until Processing ([⬆️](#queues--jobs-tips-cd-))

Sometimes, you may have jobs where only one job can be queued at a time, but once it starts processing, you can queue more jobs. Laravel ships with the "ShouldBeUniqueUntilProcessing" contract to do exactly this 🚀

```php
<?php
 
use App\Models\Product;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Contracts\Queue\ShouldBeUniqueUntilProcessing;
 
class UpdateSearchIndex implements ShouldQueue, ShouldBeUniqueUntilProcessing
{
    // ...
}
```

## Laravel Tip 💡: Rate Limit Jobs ([⬆️](#queues--jobs-tips-cd-))

Have you ever needed to rate-limit a job? Whether to avoid overwhelming an API or to limit free plan users from running too many jobs, Laravel allows you to define rate limiters and use them out of the box 🚀

```php
<?php

use Illuminate\Cache\RateLimiting\Limit;
use Illuminate\Support\Facades\RateLimiter;
use Illuminate\Queue\Middleware\RateLimited;

// In one of your service providers
RateLimiter::for('reports', function (object $job) {
    return $job->user->vipCustomer()
        ? Limit::none()
        : Limit::perHour(5)->by($job->user->id);
});


// In your job class
public function middleware(): array
{
    return [new RateLimited('reports')];
}
```

## Laravel Tip 💡: Monitor Failed Jobs ([⬆️](#queues--jobs-tips-cd-))

Have you ever needed to keep an eye on failed jobs and get notified when that happens? The failing method allows you to do exactly that 🚀

```php
<?php

namespace App\Providers;

use Illuminate\Support\Facades\Queue;
use Illuminate\Support\ServiceProvider;
use Illuminate\Queue\Events\JobFailed;
use App\Jobs\Contracts\ShouldNotifyOnFailures;

class AppServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        Queue::failing(function (JobFailed $event) {
            $event->exception->getMessage(); // Exception message
            $event->job->getName(); // Job class
            $event->job->getRawBody(); // Job body
            $event->exception->getTraceAsString(); // Exception trace

            // You can even mark the jobs with a contract to decide 
            // whether to send notifications or not 🔥
            if ($event->job instanceof ShouldNotifyOnFailures) {
                $notifiable->notify(new JobFailedNotification($event));
            }
        });
    }
}
```

## Laravel Tip 💡: Fail Jobs on Specific Exceptions ([⬆️](#queues--jobs-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D%2012.19-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

Have you ever needed to fail a job only for specific exceptions and ended up using a try-catch block with a "fail()" call?
Since Laravel v12.19, you can handle this more elegantly by using the new "FailOnException" middleware 🚀

```diff
<?php

namespace Modules\Content\Jobs;

use DateTime;
use Throwable;
use Illuminate\Foundation\Queue\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Bus\Dispatchable;

class ProcessContentTranslation implements ShouldQueue
{
    use Dispatchable, Queueable;

    public function __construct(
        private readonly Content $content,
    ) {
    }

    public function handle(TranslateContent $action): void
    {
-        try {
            $action->handle($this->content);
-        } catch (Throwable $exception) {
-            if ($exception instanceof InvalidContentFormatException) {
-                $this->fail($exception);
-
-                return;
-            }
-
-            throw $exception;
-        }
    }

    public function retryUntil(): DateTime
    {
        return now()->addHours(5);
    }

+    public function middleware(): array
+    {
+        return [
+            new FailOnException([InvalidContentFormatException::class]),
+        ];
+    }
}
```

## Laravel Tip 💡: Display Remaining Attempts for a Rate-Limited Job ([⬆️](#queues--jobs-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D%208-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

If you have a rate-limited job that can be dispatched via a UI, you can greatly improve the UX by displaying how many attempts are remaining for the day 🚀

```php
<?php

namespace Modules\Content\Jobs;

use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Queue\Queueable;
use Illuminate\Queue\Middleware\RateLimited;

class ProcessContentTranslation implements ShouldQueue
{
    use Queueable;

    public function handle(): void
    {
        // Main job logic
    }

    public function middleware(): array
    {
        // Apply your rate limiter
        return [new RateLimited('content-translation-limiter')];
    }
}

// Then, in your UI (like Filament), you can show how many attempts remain for the day 🔥
Action::make('translate_content')
    ->label('Translate Content')
    ->icon('heroicon-o-language')
    // ... define the action here
    ->tooltip(RateLimiter::remaining(md5('content-translation-limiter'), 10) . ' remaining.');
```

## Laravel Tip 💡: Encrypt Your Jobs ([⬆️](#queues--jobs-tips-cd-))

If you are working with sensitive jobs, you can instruct Laravel to encrypt the payload by using the "ShouldBeEncrypted" interface. How cool is this? 🚀

```php
<?php

namespace App\Jobs;

use Illuminate\Foundation\Queue\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Contracts\Queue\ShouldBeEncrypted;

class ProcessPlaidTransaction implements ShouldQueue, ShouldBeEncrypted
{
    use Queueable;

    public function handle(): void
    {
        //
    }
}
```

## Laravel Tip 💡: Global Middleware for Jobs ([⬆️](#queues--jobs-tips-cd-))

Did you know you can apply global job middleware? It can be really useful for custom logging and monitoring, like instantly notifying Slack or Discord about slower-than-usual jobs 🚀

```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Facades\Bus;
use App\Jobs\Middleware\MonitorJobPerformance;

class AppServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        // Custom middleware that notifies Slack, Discord, etc. about slow jobs
        // It will be executed as the last middleware in the stack
        Bus::pipeThrough([MonitorJobPerformance::class]);
    }
}
```
