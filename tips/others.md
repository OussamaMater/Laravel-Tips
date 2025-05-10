# Other Useful Tips ([cd ..](../README.md))

- [isset()](#laravel-tip--isset-️)
- [Preview Mailables](#laravel-tip--preview-mailables-️)
- [PHP Tip 💡: More Readable Numbers](#php-tip--more-readable-numbers-️)
- [Bootable Traits](#laravel-tip--bootable-traits-️)
- [Requests Fingerprints](#laravel-tip--requests-fingerprints-️)
- [Work with IPs](#laravel-tip--work-with-ips-️)
- [The Conditionable Trait](#laravel-tip--the--conditionable-trait-️)
- [On-Demand Notifications](#laravel-tip--on-demand-notifications-️)
- [Send All Mail to a Specific Email](#laravel-tip--send-all-mail-to-a-specific-email-️)
- [The New Flexible Cache Method](#laravel-tip--the-new-flexible-cache-method-️)
- [Retrieve and Delete Items From the Session](#laravel-tip--retrieve-and-delete-items-from-the-session-️)
- [On-Demand Storage Disks](#laravel-tip--on-demand-storage-disks-️)
- [Higher Order Messages with Conditionables](#laravel-tip--higher-order-messages-with-conditionables-️)
- [First Class Callables](#php-tip--first-class-callables-️)
- [Control Notification Delivery](#laravel-tip--control-notification-delivery-️)
- [Wrap Configs in Classes](#laravel-tip--wrap-configs-in-classes-️)

## Laravel Tip 💡: isset() ([⬆️](#other-useful-tips-cd-))

Did you know you could pass multiple arguments to the isset() function?

```php
<?php

if(isset($var1) && isset($var2)) { ... }
if(isset($var1, $var2)) { ... }
```

## Laravel Tip 💡: Preview Mailables ([⬆️](#other-useful-tips-cd-))

When working with mailables, we often send them to MailHog or Mailtrap to quickly preview the rendered email. Did you know that Laravel allows you to preview emails in the browser as if they were regular Blade files? 🚀

```php
<?php

Route::get('/mailable', function () {
    $invoice = App\Models\Invoice::find(1);

    return new App\Mail\InvoicePaid($invoice);
});
```

## PHP Tip 💡: More Readable Numbers ([⬆️](#other-useful-tips-cd-))

If you work with numbers, the longer they are, the harder they are to read. Did you know you can use underscores for better readability? 🚀

```php
<?php

$amount = 1000;
$amount = 1_000;

$amount = 100000;
$amount = 100_000;

$amount = 100000000;
$amount = 100_000_000;
```

## Laravel Tip 💡: Bootable Traits ([⬆️](#other-useful-tips-cd-))

Did you know that Laravel automatically boots your traits if they follow the `boot[TraitName]` convention? This allows you to easily define shared logic for model events. And here's a secret: that's where multi-tenancy starts 🚀

```php
<?php

trait Sluggable
{
    public static function bootSluggable()
    {
        static::saving(function ($model) {
            $model->slug = str($model->title)->slug()->toString();
        });
    }
}

class Post extends Model
{
    use Sluggable; // The trait will be booted automatically
}
```

## Laravel Tip 💡: Requests Fingerprints ([⬆️](#other-useful-tips-cd-))

Have you ever needed to code a unique identifier for a request, such as for caching purposes? Laravel ships with the "fingerprint" method that allows you to generate a unique identifier for your requests 🚀

```php
<?php

// Generates a unique fingerprint using the domain, URI, method and IP address
request()->fingerprint() // fbb969117edfa916b86dfb67fd11decf1e336df0
```

## Laravel Tip 💡: Work with IPs ([⬆️](#other-useful-tips-cd-))

Sometimes you may need to work with IP addresses. Laravel uses the `HttpFoundation` component from Symfony under the hood, which comes with useful IP helpers 🚀

```php
use Symfony\Component\HttpFoundation\IpUtils;

$ipv4 = '192.168.1.1';

IpUtils::checkIp4($ipv4); // true, "checkIp6" is also available
IpUtils::isPrivateIp($ipv4); // true, works with IPv6 as well
IpUtils::anonymize($ipv4); // '192.168.1.0', works with IPv6 as well
```

## Laravel Tip 💡: The  Conditionable Trait ([⬆️](#other-useful-tips-cd-))

Do you find yourself writing multiple if statements to call different methods on a class? Consider making your class "conditionable" by using Laravel's "Conditionable" trait 🚀

```php
<?php

use Illuminate\Support\Traits\Conditionable;

class NotificationService
{
    use Conditionable;

    public function sendEmailNotification()
    {
        echo "Email notification sent.";
    }

    public function sendSmsNotification()
    {
        echo "SMS notification sent.";
    }
}

$notificationService = new NotificationService;

$shouldSendEmail = true;
$shouldSendSms = false;

// Instead of this
if ($shouldSendEmail) {
    $notificationService->sendEmailNotification();
}

if ($shouldSendSms) {
    $notificationService->sendSmsNotification();
}

// You can do this
$notificationService
    ->when($shouldSendEmail, fn(NotificationService $service) => $service->sendEmailNotification())
    ->when($shouldSendSms, fn(NotificationService $service) => $service->sendSmsNotification());
```

## Laravel Tip 💡: On-Demand Notifications ([⬆️](#other-useful-tips-cd-))

Sometimes, you may want to send notifications to "anonymous" users who are not yet stored in the database. Laravel's "route" method allows you to do exactly that 🚀

```php
<?php

use Illuminate\Broadcasting\Channel;
use Illuminate\Support\Facades\Notification;

Notification::route('mail', 'john@example.com')
    ->route('twilio', '9419287384')
    ->route('slack', '#slack-channel')
    ->notify(new InvoicePaid($invoice));
```

## Laravel Tip 💡: Send All Mail to a Specific Email ([⬆️](#other-useful-tips-cd-))

Ever needed to send all mails to a single address? Whether you're working in a specific environment or managing a small project with just one contact email, you can use the "alwaysTo" method to do exactly that 🚀

```php
<?php

use Illuminate\Support\Facades\Mail;

public function boot(): void
{
    if (app()->environment('staging')) {
        Mail::alwaysTo('company@domain.com');
    }
}
```

## Laravel Tip 💡: The New Flexible Cache Method ([⬆️](#other-useful-tips-cd-))

Starting with Laravel v11.23.0, you can use the new "flexible" method for caching. If you've struggled with revalidating your cache before it expires, make use of it 🚀

```php
<?php

// If a request is made between the 5 and 10s interval,
// the cache will be recalculated 🔥 The cache will only expire after 10 seconds
// if no requests are made within the 5 to 10s window.
$value = Cache::flexible('users', [5, 10], fn () => User::all());
```

## Laravel Tip 💡: Retrieve and Delete Items From the Session ([⬆️](#other-useful-tips-cd-))

We often need to retrieve an item from the session and then delete it. While you can use the usual combo of get and forget, Laravel ships with the "pull" method that does exactly that 🚀

```php
<?php

// Instead of this 😫
$value = session()->get('key', 'default-value');

session()->forget('key');

// Do this 😎
$value = session()->pull('key', 'default-value');
```

## Laravel Tip 💡: On-Demand Storage Disks ([⬆️](#other-useful-tips-cd-))

Have you ever needed to quickly create a disk, whether for tests or temporary files, but had to define it in the filesystem configuration? Well, Laravel ships with on-demand disks so that you can define disks at runtime instead 🚀

```php
<?php

use Illuminate\Support\Facades\Storage;
 
$disk = Storage::build([
    'driver' => 'local',
    'root' => '/path/to/root',
]);
 
$disk->put('image.jpg', $content);
```

## Laravel Tip 💡: Higher Order Messages with Conditionables ([⬆️](#other-useful-tips-cd-))

If you are using the Conditionable trait in your classes or working with a Conditionable class like "Str", you can make use of higher order messages for an even more fluent API 🚀

```php
<?php

// Instead of passing a callback
Str::of("test@example.com")->when(
  Str::of("test@example.com")->contains("@"),
  fn(string $str) => $str->append(" (email)")
);

// You can use high order message, much more fluent 🔥
Str::of("test@example.com")
  ->when->contains("@") // use when() instead on your custom conditionable classes
  ->append(" (email)");
```

## PHP Tip 💡: First Class Callables ([⬆️](#other-useful-tips-cd-))

PHP 8.1 introduced first class callables. They can add syntactic sugar especially when working with Laravel collections, where closures are commonly used 🚀

```php
<?php

public function handle(): void
{
    $this->comments
        // Instead of this 🥱
        ->filter(fn (Comment $comment) => $this->isSpam($comment))
        // You can use first class callables
        ->filter($this->isSpam(...))
        
}

private function isSpam(Comment $comment): bool
{
    // Check if the comment is a spam
}
```

## Laravel Tip 💡: Control Notification Delivery ([⬆️](#other-useful-tips-cd-))

There are times when you may need to determine whether a queued notification should be sent to the user, such as when users can opt out of notifications. Laravel ships with the "shouldSend" to do exactly that 🚀

```php
<?php

namespace App\Notifications;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Notifications\Notification;

class MarketingNotification extends Notification implements ShouldQueue
{
    use Queueable;

    // ...

    public function shouldSend(object $notifiable, string $channel): bool
    {
        // If false, the notification won't be sent
        return $this->notiable->notifications_enabled;
    }
}
```

## Laravel Tip 💡: Wrap Configs in Classes ([⬆️](#other-useful-tips-cd-))

Laravel configs often get reused across the codebase, which can become painful to manage. Instead, group related configs in a class for cleaner, easier maintenance 🚀

```php
<?php

namespace App\Support\Config;

use Exception;

final class ScrapingBeeConfig
{
    public static function isEnabled(): bool
    {
        return config()->boolean('services.scrapingbee.enabled');
    }

    public function getApiKey(): string
    {
        return config()->string('services.scrapingbee.api_key');
    }

    public function getApiUrl(): string
    {
        return config()->string('services.scrapingbee.api_url');
    }

    public function isConfigured(): bool
    {
        return config('services.scrapingbee.api_key') !== null && config('services.scrapingbee.api_url') !== null;
    }

    public function ensureConfigured(): void
    {
        if (! self::isConfigured()) {
            throw new Exception('ScrapingBee is not configured');
        }
    }
}

Route::get('/', function () {
    // Using this in many places becomes painful overtime
    return config('services.scrapingbee.enabled');

    // With a dedicated class, your config becomes cleaner and much easier 
    // to manage and update
    return ScrapingBeeConfig::isEnabled();
});
```
