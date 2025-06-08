# Artisan & Console Commands Tips ([cd ..](../README.md))

- [Much Cooler Command Output](#laravel-tip--much-cooler-command-output-️)
- [The Scheduler's "skip" Method](#laravel--the-schedulers-skip-method)
- [On Command Result](#laravel-tip--on-command-result-️)
- [Command Input Auto-Completion](#laravel-tip--command-input-auto-completion-️)
- [Mail Command Output](#laravel-tip--mail-command-output-️)
- [Hide Console Commands](#laravel-tip--hide-console-commands-️)
- [Chain Scheduled Commands](#laravel-tip--chain-scheduled-commands-️)
- [Schedule Jobs Based On Time Zones](#laravel-tip--schedule-jobs-based-on-time-zones-️)
- [Run Commands In Maintenance Mode](#laravel-tip--run-commands-in-maintenance-mode-️)
- [Run Commands In the Background](#laravel-tip--run-commands-in-the-background-️)
- [Schedule Shell Commands](#laravel-tip--schedule-shell-commands-️)
- [Ping URLs When Running Commands](#laravel-tip--ping-urls-when-running-commands-️)
- [Schedule Commands on Specific Environments](#laravel-tip--schedule-commands-on-specific-environments-️)
- [Connect to Your DB via Artisan](#laravel-tip--connect-to-your-db-via-artisan-️)
- [Ensure Proper Table Name in Migrations](#laravel-tip--ensure-proper-table-name-in-migrations-️)
- [Cool Artisan DB Commands](#laravel-tip--cool-artisan-db-commands-️)
- [Ask for Confirmation in Commands](#laravel-tip--ask-for-confirmation-in-commands-️)
- [Show Model Infos](#laravel-tip--show-model-infos-️)
- [Define Command Aliases](#laravel-tip--define-command-aliases-️)
- [Email Command Failures Automatically](#laravel-tip--email-command-failures-automatically-️)
- [The Prohibitable Trait](#laravel-tip--the-prohibitable-trait-️)
- [Prohibit DB Destructive Commands](#laravel-tip--prohibit-db-destructive-commands-️)
- [Conditionally Hide Console Commands](#laravel-tip--conditionally-hide-console-commands-️)
- [Run Scheduled Commands on a Single Server](#laravel-tip--run-scheduled-commands-on-a-single-server-️)
- [Handle Command Output](#laravel-tip--handle-command-output-️)
- [Prompt For Missing Arguments](#laravel-tip--prompt-for-missing-arguments-️)
- [Confirm to Proceed](#laravel-tip--confirm-to-proceed-️)

## Laravel Tip 💡: Much Cooler Command Output ([⬆️](#artisan--console-commands-tips-cd-))

It is true that Laravel provides methods like "info()" and "error()" to send output to the console, but since Laravel 9, the core itself started using "termwind", which you can see when seeding your database or in case of an error, and you can leverage that as well by using the "components" attributes.

```php
<?php

/**
 * Execute the console command.
 */
public function handle()
{
    // A standard error message
    $this->error('The old fashioned way.');

    // A much cooler error message
    $this->components->error('What Laravel uses internally.');

    // And more
    $this->components->info('Hello, World!');
    $this->components->warn('Hello, World!');
    $this->components->alert('Hello, World!');
    // choice, confirm, ask, warn, task, line, bulletList ..

    return Command::SUCCESS;
}
```

## Laravel 💡: The Scheduler's "skip" Method

Sometimes, you might want to skip executing a command based on a specific condition. Laravel includes the "skip" method to accomplish exactly that 🚀

```php
<?php

$schedule->command('emails:send')->daily()->skip(function () {
    return Carbon::today()->isHoliday();
});
```

## Laravel Tip 💡: On Command Result ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that Laravel allows you to define callbacks to be executed based on the result of a scheduled task? This helps log failures or execute related actions on success 🚀

```php
<?php

use Illuminate\Console\Scheduling\Schedule;

$schedule->command('emails:send')
            ->daily()
            ->onSuccess(function () {
                // The task succeeded...
               })
            ->onFailure(function () {
                 // The task failed...
            });
```

## Laravel Tip 💡: Command Input Auto-Completion ([⬆️](#artisan--console-commands-tips-cd-))

When building console commands, you can improve the user experience by implementing auto-completion for the user. This can be done using the "anticipate" method provided by Laravel 🚀

```php
<?php

// You can use arrays 
$animal = $this->anticipate("What's your favourite animal?", ['dogs', 'cats']);

// Or run a closure, triggered every time a user types a character
$animal = $this->anticipate("What's your favourite animal?", function (string $input) {
    return Animal::query()
                ->where('name', 'LIKE', "$input%")
                ->pluck('name')
                ->toArray();
});
```

## Laravel Tip 💡: Mail Command Output ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that the Laravel scheduler allows you to email the output of a command to an email address of your choosing? 🚀

```php
<?php

$schedule->command(SendEmailsCommand::class)
    ->daily()
    ->emailOutputTo('oussama@example.com');

// You can also use `emailOutputOnFailure`.
```

## Laravel Tip 💡: Hide Console Commands ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that you can conditionally hide console commands? This is useful when you are building packages and you want a command to be executed only once 🚀

```php
<?php

namespace Package\Commands;

use Illuminate\Console\Command;
use Illuminate\Support\Facades\Artisan;
use Package\PackageServiceProvider;

class Install extends Command
{
    protected $signature = 'package:install';

    public function __construct()
    {
        parent::__construct();

        if (file_exists(config_path('package-config.php'))) {
            $this->setHidden();
        }
    }

    public function handle()
    {
        Artisan::call('vendor:publish', ['--provider' => PackageServiceProvider::class]);
        
        $this->info('Package was installed successfully 🎉');
    }
}
```

## Laravel Tip 💡: Chain Scheduled Commands ([⬆️](#artisan--console-commands-tips-cd-))

You can chain commands in your scheduler using the `then()` method, an undocumented feature that I often find myself using 🚀

```php
<?php

$schedule->command('db:backup')
            ->daily()
            ->then(function(){
                $this->command('notify:slack');
            });
```

## Laravel Tip 💡: Schedule Jobs Based On Time Zones ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that you can schedule jobs based on specific time zones? You can do so by chaining the "timezone" method 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;

Schedule::command('report:generate')
    ->timezone('Africa/Tunis')
    ->at('9:00')
```

## Laravel Tip 💡: Run Commands In Maintenance Mode ([⬆️](#artisan--console-commands-tips-cd-))

When Laravel's maintenance mode is on, all scheduled commands won't run. If you wish to change this behavior, you can chain the "evenInMaintenanceMode()" method 🚀

```php
<?php

// Command will run even when maintenance mode is on
Schedule::command('emails:send')->evenInMaintenanceMode();
```

## Laravel Tip 💡: Run Commands In the Background ([⬆️](#artisan--console-commands-tips-cd-))

Scheduled commands run sequentially. If you have a long-running task, it could take longer than anticipated and cause a delay for other tasks. Luckily, in such cases, you can use the "runInBackground" method 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;

Schedule::command('analytics:report')
        ->daily()
        ->runInBackground();
```

## Laravel Tip 💡: Schedule Shell Commands ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that the Laravel Scheduler allows you to execute commands in the operating system? 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;
 
Schedule::exec('node /home/forge/script.js')->daily();
```

## Laravel Tip 💡: Ping URLs When Running Commands ([⬆️](#artisan--console-commands-tips-cd-))

Did you know you can ping URLs before and after your command has run? This is really useful if you want to notify an external service or a webhook. 🚀

```php
<?php

Schedule::command('emails:send')
    ->daily()
    ->pingBefore($webhookUrl)
    ->thenPing($webhookUrl);
```

## Laravel Tip 💡: Schedule Commands on Specific Environments ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that you can schedule your commands for specific environments? If you frequently use "schedule:work", you'll find this helpful for excluding commands from the dev environment 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;

Schedule::command('newsletter:send')
    ->environments('production') // You can also pass an array of environments
    ->weekends();
```

## Laravel Tip 💡: Connect to Your DB via Artisan ([⬆️](#artisan--console-commands-tips-cd-))

Ever needed to quickly connect to your database via the CLI? There’s an Artisan command to do exactly that! 🚀

```php
// This will connect you directly to the database
php artisan db

// Have multiple connections? No worries you can specify which one to use
php artisan db mysql
```

## Laravel Tip 💡: Ensure Proper Table Name in Migrations ([⬆️](#artisan--console-commands-tips-cd-))

When creating migrations, we sometimes don't format the name in a way that Laravel can understand to fill in the table name. However, you can always specify it manually 🚀

```php
<?php

/**
 * If you want Laravel to fill in the Schema::table() for you,
 * use the --table argument when generating the migration.
 */
php artisan make:migration "tweak_users_table" --table=users

return new class extends Migration
{
    public function up(): void
    {
        Schema::table('users', function (Blueprint $table) {
            //
        });
    }

    public function down(): void
    {
        Schema::table('users', function (Blueprint $table) {
            //
        });
    }
};
```

## Laravel Tip 💡: Cool Artisan DB Commands ([⬆️](#artisan--console-commands-tips-cd-))

Have you ever needed to check if your db connection is working as expected? Or wondered how many open connections you have? Maybe you want to know the total size of a db? Well, Artisan comes with some cool commands to do exactly that 🚀

```php
# This command allows you to inspect a table
php artisan db:table

# This command checks if your db connections are working
php artisan db:monitor

# This command displays the db version, total size, open connections, and more
php artisan db:show
```

## Laravel Tip 💡: Ask for Confirmation in Commands ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that you can request confirmation for risky commands before executing them? You can do this using the "confirm" method 🚀

```php
<?php

// Displays the old Laravel prompt view
$this->confirm('Do you want to continue?');

// With "components", it displays the modern Laravel prompt view
$this->components->confirm('Do you want to continue?');

// In your terminal, you should see
/*
 * Do you want to continue? (yes/no) [no]
 *
 */
```

## Laravel Tip 💡: Show Model Infos ([⬆️](#artisan--console-commands-tips-cd-))

When a model grows, it can be hard to check all the relationships, including those from third-party packages, the registered events, and the observers. When that's the case, you can use the "model:show" command instead 🚀

```shell
php artisan model:show User

# This will list: The table, attributes, relationships, events and observers.
```

## Laravel Tip 💡: Define Command Aliases ([⬆️](#artisan--console-commands-tips-cd-))

We've all created custom Artisan commands for different purposes. While it's great to have an expressive signature, if you're using the command often, you can define an alias for it 🚀

```php
<?php

class BillReminder extends Command
{
    protected $signature = 'reminder:bill';

    protected $aliases = ['rb']; // Alias here

    // ...
}

// You can run the command with:
// php artisan reminder:bill

// But now you can also use the alias
// php artisan rb
```

## Laravel Tip 💡: Email Command Failures Automatically ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that Laravel ships with the "emailOutputOnFailure" method which automatically sends the output of a failed command to your email? 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;

Schedule::command('report:generate')
         ->daily()
         ->emailOutputOnFailure(config('contact.support'));
```

## Laravel Tip 💡: The Prohibitable Trait ([⬆️](#artisan--console-commands-tips-cd-))

Most Laravel apps often have local-only or environment-dependent commands that shouldn't run elsewhere. To prevent accidents, use the "Prohibitable" trait and call the "prohibit" method 🚀

```php
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Console\Prohibitable;

class CleanLogs extends Command
{
    use Prohibitable;
}

// Now in the boot method of the AppServiceProvider
CleanLogs::prohibit(app()->isProduction());
```

## Laravel Tip 💡: Prohibit DB Destructive Commands ([⬆️](#artisan--console-commands-tips-cd-))

Running migrations or wiping the DB in production can be, well, disastrous. Since Laravel v11, you can prohibit all DB destructive commands by calling "prohibitDestructiveCommands" method 🚀

```php
<?php

namespace App\Providers;

use Illuminate\Support\Facades\DB;
use Illuminate\Support\ServiceProvider;

class AppServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        // Prevents 'migrate:fresh', 'migrate:refresh', 'migrate:reset', and 'db:wipe'
        DB::prohibitDestructiveCommands(
            $this->app->isProduction()
        );
    }
}
```

## Laravel Tip 💡: Conditionally Hide Console Commands ([⬆️](#artisan--console-commands-tips-cd-))

Sometimes, you may want to hide console commands, such as legacy commands, from being listed. While you can manually hide them using the `setHidden()`, you can do this with the `isHidden()` method 🚀

```php
<?php
 
namespace App\Console\Commands;
 
use Illuminate\Console\Command;
 
class LegacyCommand extends Command
{
    // ...

    public function isHidden(): bool
    {
        // This could check a configuration flag
        return true;
    }
}
```

## Laravel Tip 💡: Run Scheduled Commands on a Single Server ([⬆️](#artisan--console-commands-tips-cd-))

Running your app on multiple servers? By default, scheduled commands will execute on all servers, which is unnecessary and can cause issues. You can prevent this by using the "onOneServer" 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;

Schedule::command('report:generate')
    ->fridays()
    ->at('17:00')
    ->onOneServer(); // the command will run on a single server
```

## Laravel Tip 💡: Handle Command Output ([⬆️](#artisan--console-commands-tips-cd-))

Did you know that Laravel's scheduler allows you to save or append a command’s output to a specific file? 🚀

```php
<?php

use Illuminate\Support\Facades\Schedule;
 
Schedule::command('emails:send')
    ->daily()
    ->sendOutputTo($filePath);
    
// You can also append the output 🔥
Schedule::command('emails:send')
    ->daily()
    ->appendOutputTo($filePath);
```

## Laravel Tip 💡: Prompt for Missing Arguments ([⬆️](#artisan--console-commands-tips-cd-))

Have you ever needed to ensure users provide the required console arguments? Laravel ships with the "PromptsForMissingInput" contract to automatically prompt the user for missing input 🚀

```php
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Contracts\Console\PromptsForMissingInput;

class SendEmails extends Command implements PromptsForMissingInput
{
    /**
     * @var string
     */
    protected $signature = 'mail:send {user}';

    public function handle(): void
    {
        $user = $this->argument('user');

        // ...
    }
}

/**
 * If the "user" argument is not provided, Laravel automatically prompts for it 🔥
 * php artisan mail:send
 * 
 ┌ What is the user? ───────────────────────────────────────────┐
 │ oussama                                                      │
 └──────────────────────────────────────────────────────────────┘
*/
```

## Laravel Tip 💡: Confirm to Proceed ([⬆️](#artisan--console-commands-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D%204.2-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

Need to confirm before running a command? Laravel ships with the "ConfirmableTrait" for that exactly. Just call "confirmToProceed()" for confirmation, and skip the prompt anytime with the "--force" option 🚀

```php
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;
use Illuminate\Console\ConfirmableTrait;

class DeleteInactiveUsers extends Command
{
    use ConfirmableTrait;

    protected $signature = 'users:delete-inactive {--force}';

    protected $description = 'Delete all users who have been inactive for over a year.';

    public function handle(): int
    {
        if (! $this->confirmToProceed()) {
            return static::FAILURE;
        }

        // ...

        return static::SUCCESS;
    }
}

// You can then run:
// php artisan users:delete-inactive
// This will prompt you to confirm whether you want to proceed.

// You can even bypass the confirmation by using the --force option. The trait supports that 🔥
// php artisan users:delete-inactive --force
```
