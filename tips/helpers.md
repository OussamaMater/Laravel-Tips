# Helpers Tips ([cd ..](../README.md))

- [The "squish" method](#laravel-tip--the-squish-method-️)
- [The "json" method](#laravel-tip--the-json-method-️)
- [The "rescue" Helper](#laravel-tip--the-rescue-helper-️)
- [The "scan" Helper](#laravel-tip--the-scan-helper-️)
- [The New "once" Helper](#laravel-tip--the-new-once-helper-️)
- [The "throw\_if" and "throw\_unless" Helpers](#laravel-tip--the-throw_if-and-throw_unless-helpers-️)
- [The "blank" and "filled" Helpers](#laravel-tip--the-blank-and-filled-helpers-️)
- [The "Lottery" Class](#laravel-tip--the-lottery-class-️)
- [The "Sleep" Helper](#laravel-tip--the-sleep-helper-️)
- [The "back" Helper](#laravel-tip--the-back-helper-️)
- [The "words" Helper](#laravel-tip--the-words-helper-️)
- [The "Benchmark" Helper](#laravel-tip--the-benchmark-helper-️)
- [Mask Strings](#laravel-tip--mask-strings-️)
- [Human Readable Dates](#laravel-tip--human-readable-dates-️)
- [The "whenFilled" Method](#laravel-tip--the-whenfilled-method-️)
- [The "startOfHour" Method](#laravel-tip--the-startofhour-method-️)
- [Spell Numbers](#laravel-tip--spell-numbers-️)
- [Human-readable Numbers](#laravel-tip--human-readable-numbers-️)
- [The "literal" Helper](#laravel-tip--the-literal-helper-️)
- [The "abort\_if" Helper](#laravel-tip--the-abort_if-helper-️)
- [Append and Prepend to files](#laravel-tip--append-and-prepend-to-files-️)
- [Formatting to Percentages](#laravel-tip--formatting-to-percentages-️)
- [Formatting to a Human-Readable File Size](#laravel-tip--formatting-to-a-human-readable-file-size-️)
- [Working with Base64 Strings](#laravel-tip--working-with-base64-strings-️)
- [The "abort\_unless" Helper](#laravel-tip--the-abort_unless-helper-️)
- [Typed Configs](#laravel-tip--typed-configs-️)
- [Pluralize Words](#laravel-tip--pluralize-words-️)
- [Generate Random Passwords](#laravel-tip--generate-random-passwords-️)
- [Abbreviate Numbers](#laravel-tip--abbreviate-numbers-️)
- [The New "chopStart" and "chopEnd" Methods](#laravel-tip--the-new-chopstart-and-chopend-methods-️)
- [Swap Multiple Strings](#laravel-tip--swap-multiple-strings-️)
- [Count the Words](#laravel-tip--count-the-words-️)
- [The "last" and "head" helpers](#laravel-tip--the-last-and-head-helpers-️)
- [Filter Null Values](#laravel-tip--filter-null-values-️)
- [Truncate Long Strings](#laravel-tip--truncate-long-strings-️)
- [Deduplicate Characters](#laravel-tip--deduplicate-characters-️)
- [Ensure Env Keys Exist](#laravel-tip--ensure-env-keys-exist-️)
- [Safer Passwords for Users](#laravel-tip--safer-passwords-for-users-️)
- [Auto Capitalize Your Translations](#laravel-tip--auto-capitalize-your-translations-️)
- [The "data\_get" Helper](#laravel-tip--the-data_get-helper-️)
- [The Pipeline Helper](#laravel-tip--the-pipeline-helper-️)
- [The "tap" Helper](#laravel-tip--the-tap-helper-️)
- [Execute Tasks Concurrently](#laravel-tip--execute-tasks-concurrently-️)
- [A Better dd()](#laravel-tip--a-better-dd-️)
- [The "today()" Helper](#laravel-tip--the-today-helper-️)
- [Get the Age of a Date](#laravel-tip--get-the-age-of-a-date-️)
- [Get the Closest and Farthest Dates](#laravel-tip--get-the-closest-and-farthest-dates-️)
- [File Checksum](#laravel-tip--file-checksum-️)
- [The "shortRelativeDiffForHumans" Method](#laravel-tip--the-shortrelativediffforhumans-method-️)
- [The "finish" Helper](#laravel-tip--the-finish-helper-️)
- [The "diffInDaysFiltered" Method](#laravel-tip--the-diffindaysfiltered-method-️)
- [The "isBirthday" Method](#laravel-tip--the-isbirthday-method-️)
- [The "headline" Method](#laravel-tip--the-headline-method-️)
- [Sort Arrays Recursively](#laravel-tip--sort-arrays-recursively-️)
- [The "data\_forget" Helper](#laravel-tip--the-data_forget-helper-️)
- [The New "doesntContain" String Method](#laravel-tip--the-new-doesntcontain-string-method-️)
- [Spell Ordinal Numbers](#laravel-tip--spell-ordinal-numbers-️)
- [The "keyBy" Method](#laravel-tip--the-keyby-method-️)
- [The "remove" Str Method](#laravel-tip--the-remove-str-method-️)
- [Check If a String Is a URL](#laravel-tip--check-if-a-string-is-a-url-️)
- [Extract Text Between Strings](#laravel-tip--extract-text-between-strings-️)
- [Reusable Pipelines](#laravel-tip--reusable-pipelines-️)
- [Clamp Numbers](#laravel-tip--clamp-numbers-️)
- [Date Checks with Carbon](#laravel-tip--date-checks-with-carbon-️)
- [Handle Pluralization Elegantly](#laravel-tip--handle-pluralization-elegantly-️)

## Laravel Tip 💡: The "squish" method ([⬆️](#helpers-tips-cd-))

I'm sure you've trimmed a string at least once. While the built-in "trim" function that PHP provides is good, it may not be sufficient if you want to eliminate extra spaces between text. In such cases, give the "squish" method a go 🚀

```php
<?php

use Illuminate\Support\Str;

$joke = Str::squish(' PHP is dead 🤣 ');

// PHP is dead 🤣 
```

## Laravel Tip 💡: The "json" method ([⬆️](#helpers-tips-cd-))

If you are using Laravel 10 and upwards, there is an elegant way to read JSON files by using "File::json()". You can also pass the flags that you would normally pass to "json_decode()", in case you want to throw an exception 🚀

```php
<?php

// Laravel < 10
$data = json_decode(File::get('data.json'), flags: JSON_THROW_ON_ERROR);

// Laravel >= 10
$data = File::json('data.json', JSON_THROW_ON_ERROR);
```

## Laravel Tip 💡: The "rescue" Helper ([⬆️](#helpers-tips-cd-))

Sometimes we are forced to use a try-catch block just to ignore an expected exception that an external service throws upon failure. Laravel provides a more elegant solution for such scenarios through the "rescue" helper 🚀

```php
<?php

// If an exception is thrown, we default to "en"
try {
    $language = LanguageDetector::detect($request->ip());
} catch (Exception $e) {
    $language = 'en';
}

// A cleaner way to achieve the same, and the exception will still be reported
$language = rescue(fn () => LanguageDetector::detect($request->ip()), 'en');
```

## Laravel Tip 💡: The "scan" Helper ([⬆️](#helpers-tips-cd-))

Did you know that you can use the "scan" helper to parse a string input into a collection according to a format supported by the built-in sscanf PHP function? 🚀

```php
<?php

$rgb = '#402A2A';

[$r, $g, $b] = str($rgb)->scan('#%2x%2x%2x');

// $r = 64, $g = 42, $b = 42
```

## Laravel Tip 💡: The New "once" Helper ([⬆️](#helpers-tips-cd-))

Laravel 11 has introduced a new helper called "once," which computes a result once and caches it. Subsequent calls will return the previously cached result. You can use this instead of static properties for better code readability! 🚀

```php
<?php

function random(): int
{
    return once(function () {
        return random_int(1, 1000);
    });
}

random(); // 123
random(); // 123 (cached result)
random(); // 123 (cached result)
```

## Laravel Tip 💡: The "throw_if" and "throw_unless" Helpers ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with two helpers, "throw_if" and "throw_unless," which not only make your code shorter but also much more readable? 🚀

```php
<?php

// This is okay
if (!Auth::user()->isAdmin()) {
    throw new AuthorizationException;
}

// This reads better
// Throw the exception if they're not the admin.
throw_if(!Auth::user()->isAdmin(), AuthorizationException::class);

// Throw the exception unless they're an admin.
throw_unless(Auth::user()->isAdmin(), AuthorizationException::class);
```

## Laravel Tip 💡: The "blank" and "filled" Helpers ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with two cool helpers, "blank" and "filled"? You can now have a standardized way to test if a variable is empty or not, regardless of its type. Even collections are supported! 🚀

```php
<?php

// Will return true
blank('');
blank('    ');
blank(null);
blank(collect());
blank([]);

// Will return false
blank(0);
blank('string');
blank(true);
blank(false);
blank([1]);

// For the inverse, you can make use of filled()
```

## Laravel Tip 💡: The "Lottery" Class ([⬆️](#helpers-tips-cd-))

Did you know that Laravel comes with a Lottery class that allows you to execute callbacks based on odds? I found this to be extremely helpful, especially when implementing A/B tests.

```php
<?php
use Carbon\CarbonInterval;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Lottery;

// 1 out of every 100 slow queries will be reported.
DB::whenQueryingForLongerThan(
    CarbonInterval::seconds(2),
    Lottery::odds(1, 100)->winner(fn () => report('Querying > 2 seconds.')),
);
```

## Laravel Tip 💡: The "Sleep" Helper ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with a fluent wrapper for the PHP "sleep" method? This not only makes the code readable but also testable, as you can fake the Sleep class 🚀

```php
<?php

// Pause execution for 90 seconds
Sleep::for(1.5)->minutes();

// Pause execution for 2 seconds
Sleep::for(2)->seconds();

// Pause execution for 500 milliseconds
Sleep::for(500)->milliseconds();

// Pause execution for 5,000 microseconds
Sleep::for(5000)->microseconds();

// Pause execution until a given time
Sleep::until(now()->addMinute());

// Alias of PHP's native "sleep" function
Sleep::sleep(2);

// Alias of PHP's native "usleep" function
Sleep::usleep(5000);

// You can also chain methods
Sleep::for(1)->second()->and(10)->milliseconds();
```

## Laravel Tip 💡: The "back" Helper ([⬆️](#helpers-tips-cd-))

I know we've all redirected users back at some point, and we typically use the "request()->back()" method. However, you can simply call the "back()" helper function 🚀

```php
<?php
// Instead of this
return redirect()->back($status = 302, $headers = [], $fallback = '/');

// You can do this
return back($status = 302, $headers = [], $fallback = '/');
```

## Laravel Tip 💡: The "words" Helper ([⬆️](#helpers-tips-cd-))

Sometimes, you may want to limit the number of words in a string. Well, Laravel comes with a handy helper "words" to do exactly that! 🚀

```php
<?php

use Illuminate\Support\Str;

return Str::words("Don't refactor without tests.", 2);
// Don't refactor ...

return Str::words("Don't refactor without tests.", 2, ' 👀');
// Don't refactor 👀

// You can also use fluent string 😎
return str("Don't refactor without tests.")->words(2);
// Don't refactor ...
```

## Laravel Tip 💡: The "Benchmark" Helper ([⬆️](#helpers-tips-cd-))

Did you know that Laravel 9.32 and above come with a handy helper called "Benchmark", allowing you to measure the number of milliseconds it takes for the given callbacks to complete? 🚀

```php
<?php

use App\Models\User;
use Illuminate\Support\Benchmark;

// This will measure and return the value
Benchmark::measure(fn () => User::find(1)); // 0.1 ms

// This will measure and dump the value
Benchmark::dd(fn () => User::find(1)); // 0.1 ms

// For both measure() and dd(), you can pass an array
Benchmark::dd([
    'Scenario 1' => fn () => User::count(), // 0.5 ms
    'Scenario 2' => fn () => User::all()->count(), // 20.0 ms
]);

// You can also save the values
[$count, $duration] = Benchmark::value(fn () => User::count());
```

## Laravel Tip 💡: Mask Strings ([⬆️](#helpers-tips-cd-))

Ever found yourself in need of masking an email or a verification code for security purposes? Laravel ships with the "mask" method to do exactly that! You can always combine it with other methods to avoid leaking the length of the string 🚀

```php
<?php

use Illuminate\Support\Str;

Str::mask('john@example.com', '*', 3); // joh*************
Str::mask('98552157', '*', -5, 4); // 985****7
```

## Laravel Tip 💡: Human Readable Dates ([⬆️](#helpers-tips-cd-))

>[!NOTE]
>This will work with Carbon objects.

Have you ever wanted to display human-readable dates instead of exact ones? Like "1 day ago" or "a month ago"? Laravel allows you to do exactly that by using the "diffForHumans" method 🚀

```php
<?php

// 5 days ago
$post->created_at->diffForHumans();

// 5 days 23 minutes ago
$post->created_at->diffForHumans(['parts' => 2]);

// 5 days 24 minutes 36 seconds ag
$post->created_at->diffForHumans(['parts' => 3]);
```

## Laravel Tip 💡: The "whenFilled" Method ([⬆️](#helpers-tips-cd-))

We often test whether or not a request parameter is filled to decide to perform logic. Laravel ships with a cool helper called "whenFilled" to do just that! 🚀

```php
<?php

$request->whenFilled('name', function (string $input) {
    // The "name" value is filled...
}, function () {
    // The "name" value is not filled...
});
```

## Laravel Tip 💡: The "startOfHour" Method ([⬆️](#helpers-tips-cd-))

When working with time, you may want to have a sharp hour, like 18:00:00. Since Laravel uses Carbon under the hood, you have access to "startOfHour," which does exactly that 🚀

```php
<?php
// 2024-04-26 18:46:39
echo now();

// 2024-04-26 18:46:00
echo now()->setSeconds(0);

// 2024-04-26 18:00:00
echo now()->setSeconds(0)->setMinutes(0);

// 2024-04-26 18:00:00
echo now()->startOfHour();
```

## Laravel Tip 💡: Spell Numbers ([⬆️](#helpers-tips-cd-))

Did you know that you can spell numbers in different locales using the "Number" helper that Laravel ships with? 🚀

```php
<?php

use Illuminate\Support\Number;

$number = Number::spell(102); // one hundred and two

$number = Number::spell(88, locale: 'fr'); // quatre-vingt-huit
```

## Laravel Tip 💡: Human-readable Numbers ([⬆️](#helpers-tips-cd-))

Sometimes you may want to format numbers for your users in a human-readable format. The "Number" helper allows you to do just that 🚀

```php
<?php

use Illuminate\Support\Number;
 
$number = Number::forHumans(1000); // 1 thousand
 
$number = Number::forHumans(489939); // 490 thousand
 
$number = Number::forHumans(1230000, precision: 2); // 1.23 million
```

## Laravel Tip 💡: The "literal" Helper ([⬆️](#helpers-tips-cd-))

>[!NOTE]
>You might as well check the Fluent class 🙌

Did you know that Laravel ships with a cool helper called "literal" that allows you to create a PHP object using named arguments? 🚀

```php
<?php

$obj = literal(
    name: 'Joe',
    languages: ['PHP', 'Ruby'],
);

$obj->name;      // 'Joe'
$obj->languages; // ['PHP', 'Ruby']
```

## Laravel Tip 💡: The "abort_if" Helper ([⬆️](#helpers-tips-cd-))

When writing middlewares, we often abort the request if a condition is met. For such cases, "abort_if" allows you to do exactly that! 🚀

```php
<?php

// Instead of this 😞
if (!Auth::user()->isAdmin()) {
    abort(403);
}

// Do this 😎
abort_if(!Auth::user()->isAdmin(), 403);
```

## Laravel Tip 💡: Append and Prepend to files ([⬆️](#helpers-tips-cd-))

When working with files, you may need to prepend or append content. Luckily, Laravel ships with two helpers to do exactly that 🚀

```php
<?php

Storage::prepend('file.log', 'Prepended Text');

Storage::append('file.log', 'Appended Text');
```

## Laravel Tip 💡: Formatting to Percentages ([⬆️](#helpers-tips-cd-))

Did you know Laravel ships with a "percentage" helper to get the percentage of any representative value? 🚀

```php
<?php

use Illuminate\Support\Number;
 
$percentage = Number::percentage(10); // 10%
 
$percentage = Number::percentage(10, precision: 2); // 10.00%
 
$percentage = Number::percentage(10.123, maxPrecision: 2); // 10.12%
 
$percentage = Number::percentage(10, precision: 2, locale: 'de'); // 10,00%
```

## Laravel Tip 💡: Formatting to a Human-Readable File Size ([⬆️](#helpers-tips-cd-))

Did you know Laravel ships with a "fileSize" helper to get the file size representation of a given byte value as a string? 🚀

```php
<?php

use Illuminate\Support\Number;
 
$size = Number::fileSize(1024); // 1 KB
 
$size = Number::fileSize(1024 * 1024); // 1 MB
 
$size = Number::fileSize(1024, precision: 2); // 1.00 KB
```

## Laravel Tip 💡: Working with Base64 Strings ([⬆️](#helpers-tips-cd-))

We often work with Base64 strings, especially when building API integrations. Laravel comes with built-in helpers to work with Base64 right out of the box 🚀

```php
<?php

use Illuminate\Support\Str;
 
$base64 = Str::toBase64('Laravel'); // TGFyYXZlbA==
$base64 = str('Laravel')->toBase64(); // TGFyYXZlbA==

$base64 = Str::fromBase64('TGFyYXZlbA=='); // Laravel
$base64 = str('TGFyYXZlbA==')->fromBase64(); // Laravel
```

## Laravel Tip 💡: The "abort_unless" Helper ([⬆️](#helpers-tips-cd-))

When writing middlewares, we often need to abort the request if a condition is met. For such cases, "abort_unless" allows you to do exactly that! 🚀

```php
<?php

// Instead of this 🥱
if (!Auth::user()->isAdmin()) {
    abort(403);
}

// Do this 😎
abort_unless(Auth::user()->isAdmin(), 403);
```

## Laravel Tip 💡: Typed Configs ([⬆️](#helpers-tips-cd-))

If you are using static analysis tools like PHPStan (which you should), you can make use of typed configs. Not only does this assist the tools, but it also ensures that the config matches the required type 🚀

```php
<?php

Config::string('config-key'); // config()->string('config-key')
Config::integer('config-key'); // config()->integer('config-key')
Config::float('config-key'); // config()->float('config-key')
Config::boolean('config-key'); // config()->boolean('config-key')
Config::array('config-key'); // config()->array('config-key')
```

## Laravel Tip 💡: Pluralize Words ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with the "plural" method to help you pluralize words? This is really helpful when you want to show a quantity-dependent message to your users. 🚀

```php
<?php

use Illuminate\Support\Str;

// The count is optional, if 1 is passed, the same word will be returned
$plural = Str::plural('car', count: 2); // cars

// Also available as a fluent method
$plural = str('child')->plural(); // children
```

## Laravel Tip 💡: Generate Random Passwords ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with a "password" method that generates random, strong passwords? This is helpful when you want to suggest passwords for your users 🚀

```php
<?php

use Illuminate\Support\Str;

// The password will include letters, numbers, symbols, and spaces.
// The default length is 32 characters.
$password = Str::password(); // '?;D7zlsMmZ87R0aBmIH.>GU77nagX26U'

$password = Str::password(12); // 'q_2j00<#gr{'
```

## Laravel Tip 💡: Abbreviate Numbers ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with the "abbreviate" method, which allows you to format numbers in a human-readable way, with an abbreviation for the units? 🚀

```php
<?php

use Illuminate\Support\Number;

$number = Number::abbreviate(1000); // 1K

$number = Number::abbreviate(489939); // 490K

$number = Number::abbreviate(1230000, precision: 2); // 1.23M
```

## Laravel Tip 💡: The New "chopStart" and "chopEnd" Methods ([⬆️](#helpers-tips-cd-))

Laravel 11.14 introduces 2 new string helpers that allow you to remove characters from the beginning or end of a string 🚀

```php
<?php

use Illuminate\Support\Str;
 
$url = Str::chopStart('http://laravel.com', ['https://', 'http://']); // 'laravel.com'
$url = Str::chopEnd('app/Models/Photograph.php', '.php'); // 'app/Models/Photograph'
```

## Laravel Tip 💡: Swap Multiple Strings ([⬆️](#helpers-tips-cd-))

When working with strings, we often need to find and replace occurrences of multiple strings. Laravel ships with an elegant method "swap" to do exactly that 🚀

```php
<?php

use Illuminate\Support\Str;

// The swap method is also available as a fluent method.
$string = Str::swap([
    'Tacos' => 'Burritos',
    'great' => 'fantastic',
], 'Tacos are great!');
 
// $string: Burritos are fantastic!
```

## Laravel Tip 💡: Count the Words ([⬆️](#helpers-tips-cd-))

Have you ever needed to count the words in a string? Laravel ships with the "countWords" method to do exactly that 🚀

```php
<?php

use Illuminate\Support\Str;
 
Str::wordCount('Okay, this helper is so cool!'); // 6
```

## Laravel Tip 💡: The "last" and "head" helpers ([⬆️](#helpers-tips-cd-))

Did you know that Laravel ships with two helpers, "last" and "head"? They allow you to retrieve the first and last elements of an array 🚀

```php
<?php

$array = [100, 200, 300];

$first = head($array); // 100

$last = last($array); // 300
```

## Laravel Tip 💡: Filter Null Values ([⬆️](#helpers-tips-cd-))

When working with arrays, we sometimes need to filter out null values. Laravel ships with an elegant helper "whereNotNull" to do exactly that 🚀

```php
<?php

use Illuminate\Support\Arr;

$array = [0, null, 'hello, world'];

$filtered = Arr::whereNotNull($array); // [0 => 0, 2 => "hello, world"]
```

## Laravel Tip 💡: Truncate Long Strings ([⬆️](#helpers-tips-cd-))

Sometimes you may want to truncate long descriptions for display. Laravel ships with the "limit" method to do just that, and in the upcoming version, you can preserve whole words for a better UX 🚀

```php
<?php

use Illuminate\Support\Str;

Str::limit('This will be a long description', 10); // This will ...

Str::limit('This will be a long description', 10, ' ( ... )'); // This will ( ... )

// In the upcoming Laravel version we can preserve words as well 😎
$before = Str::limit('We can preserve words', 8) // We can p...

$after = Str::limit('We can preserve words', 8, preserveWords: true) // We can...
```

## Laravel Tip 💡: Deduplicate Characters ([⬆️](#helpers-tips-cd-))

Laravel v11.20 introduces a new "deduplicate" method which allows you to remove duplicates from spaces or any character you choose 🚀

```php
<?php

Str::deduplicate('Laravel Framework') // Laravel Framework
Str::deduplicate('Laravel Frameworkkkkk', 'k') // Laravel Framework
```

## Laravel Tip 💡: Ensure Env Keys Exist ([⬆️](#helpers-tips-cd-))

If you want to be absolutely sure that a key exists in your .env file, use the "getOrFail()" method. It will throw a runtime exception if the key is missing. This is really useful for API keys 🚀

```php
<?php

use Illuminate\Support\Env;

return [
    'postmark' => [
        'token' => Env::getOrFail('POSTMARK_TOKEN'),
    ],
];

// If the POSTMARK_TOKEN key is missing from your .env file,
// an exception will be thrown with the message:
// "Environment variable [POSTMARK_TOKEN] has no value."
```

## Laravel Tip 💡: Safer Passwords for Users ([⬆️](#helpers-tips-cd-))

Users tend to use the same password for all websites, which puts them in danger if their password has been leaked. You can make sure that the user inputs an uncompromised password using the "uncompromised" rule 🚀

```php
<?php

// Under the hood, uncompromised uses the Have I Been Pwned public API
// with k-anonymity, where only a prefix of 5 characters of the hash will be sent over
Password::min(8)
    ->mixedCase()
    ->numbers()
    ->letters()
    ->uncompromised()
```

## Laravel Tip 💡: Auto Capitalize Your Translations ([⬆️](#helpers-tips-cd-))

Did you know that not only can you parameterize your translation strings, but you can also auto-capitalize them? 🚀

```php
<?php

// in your en/messages.json
return [
    'welcome' => 'Welcome, :NAME',
    'goodbye' => 'Goodbye, :Name',
];

// This will auto-capitalize it for you
echo __('messages.welcome', ['name' => 'dayle']); // Welcome, DAYLE
echo __('messages.goodbye', ['name' => 'dayle']); // Goodbye, Dayle
```

## Laravel Tip 💡: The "data_get" Helper ([⬆️](#helpers-tips-cd-))

When working with nested arrays, Laravel provides a cool helper called "data_get". This helper allows you to use "dot" syntax and wildcards to retrieve values 🚀

```php
<?php

$data = [
    'product-one' => ['name' => 'Desk 1', 'price' => 100],
    'product-two' => ['name' => 'Desk 2', 'price' => 150],
];
 
data_get($data, 'product-one.name'); // ['Desk 1'];
data_get($data, '*.name'); // ['Desk 1', 'Desk 2'];
```

## Laravel Tip 💡: The Pipeline Helper ([⬆️](#helpers-tips-cd-))

Often, we need to process input through multiple steps, such as applying request filters to a query or cleaning data in a multi-stage chain. When you find yourself in such cases, use Laravel's Pipeline helper 🚀

```php
<?php
$user = Pipeline::send($user)
    ->through([
        // Those are invokable classes
        GenerateProfilePhoto::class,
        ActivateSubscription::class,
        SendWelcomeEmail::class,
    ])
    ->then(fn(User $user) => $user);

// Example of the GenerateProfilePhoto class
class GenerateProfilePhoto
{
    public function __invoke(User $user, Closure $next)
    {
        // Execute the logic to generate the profile photo

        return $next($user);
    }
}
```

## Laravel Tip 💡: The "tap" Helper ([⬆️](#helpers-tips-cd-))

How many times have you needed to return an object right after a basic action? Yes many times I know. The "tap" helper allows you to do just that 🚀

```php
<?php
public function markAsPaid(): self
{
    // Not bad
    $this->update(['status' => 'paid']);
    return $this;

    // Better
    return tap($this)->update(['status' => 'paid']);
}
```

## Laravel Tip 💡: Execute Tasks Concurrently ([⬆️](#helpers-tips-cd-))

Starting from Laravel v11.23, you can execute tasks concurrently. This can speed things up when you have independent tasks that can be run simultaneously 🚀

```php
<?php
use App\Services\Metrics;
use Illuminate\Support\Facades\Concurrency;

Concurrency::defer([
    fn () => Metrics::report('users'),
    fn () => Metrics::report('orders'),
]);
```

## Laravel Tip 💡: A Better dd() ([⬆️](#helpers-tips-cd-))

When debugging an Eloquent query, we often use "dd()" to check the result. Did you know you can just chain it directly? 🚀

```php
<?php

// This is okay 😊
$user = User::all();
dd($users);

// This is better 🔥
User::all()->dd();
```

## Laravel Tip 💡: The "today()" Helper ([⬆️](#helpers-tips-cd-))

Sometimes you may want to get today's date. While you can do this in multiple ways, Laravel ships with a readable "today()" helper to do exactly that. You can pass timezones and chain other helpful methods as well 🚀

```php
<?php

// Returns today's date
$today = today();

// But you can do more 👀
today()->isWeekend(); // true
today()->isWeekday(); // false

today()->isSaturday(); // true, and you can check for all days
today()->isMidday(); // false

// You can also pass timezones 🔥
today($timezeone);
```

## Laravel Tip 💡: Get the Age of a Date ([⬆️](#helpers-tips-cd-))

Since Laravel uses Carbon under the hood, you can easily get the age of a parsed date 🚀

```php
<?php

use Illuminate\Support\Carbon;

// Get the age from a given date
$laravelsAge = Carbon::parse('01-06-2011')->age;

// This also works with date columns
$age = User::first()->birthday->age;
```

## Laravel Tip 💡: Get the Closest and Farthest Dates ([⬆️](#helpers-tips-cd-))

Ever needed to get the closest or farthest of two dates compared to a given date? Since Laravel uses Carbon under the hood, you can do that with the "closest" and "farthest" methods 🚀

```php
<?php

use Illuminate\Support\Carbon;

$date = Carbon::parse('2024-05-15');
$date1 = Carbon::parse('2024-01-01');
$date2 = Carbon::parse('2024-05-16');

// You can now check the closest or farthest date
$date->closest($date1, $date2); // 2024-05-16
$date->farthest($date1, $date2); // 2024-01-01
```

## Laravel Tip 💡: File Checksum ([⬆️](#helpers-tips-cd-))

Ever needed to generate a checksum for a file to check if it has been tampered with or simply to track changes over time? Laravel ships with the "checksum" method to do exactly that! 🚀

```php
<?php

// You can choose any other algo (returned by hash_algos())
Storage::checksum('/path/to/file', ['checksum_algo' => 'sha1']);
```

## Laravel Tip 💡: The "shortRelativeDiffForHumans" Method ([⬆️](#helpers-tips-cd-))

I'm sure you've used the "diffForHumans" method to get a human-readable date. But did you know you can get a shorter version using the "shortRelativeDiffForHumans" method? 🚀

```php
<?php

now()->subDays(5)->diffForHumans(); // 5 days ago

// Need a shorter version? No problem
now()->subDays(5)->shortRelativeDiffForHumans(); // 5d ago
```

## Laravel Tip 💡: The "finish" Helper ([⬆️](#helpers-tips-cd-))

Sometimes, you might need to ensure that a string ends with a specific character, like a slash or a dot. Laravel ships with the "finish" helper to do exactly that 🚀

```php
<?php

use Illuminate\Support\Str;
 
Str::finish('this/string', '/'); // this/string/

Str::finish('this/string/', '/'); // this/string/

```

## Laravel Tip 💡: The "diffInDaysFiltered" Method ([⬆️](#helpers-tips-cd-))

Ever needed to count the days between 2 dates while filtering some based on a condition? Since Laravel uses Carbon under the hood, you can use "diffInDaysFiltered" to doexactly that 🚀

```php
<?php

$start = now();
$end = now()->addDays(10);

// This will count only weekdays between the two dates 🔥
$weekdays = $start->diffInDaysFiltered(fn (Carbon $date) => !$date->isWeekend(), $end);

$weekdays; // 8
```

## Laravel Tip 💡: The "isBirthday" Method ([⬆️](#helpers-tips-cd-))

Ever needed to check whether a date is someone's birthday? Since Laravel uses Carbon under the hood, you can use the "isBirthday" method to do exactly that 🚀

```php
<?php

use Illuminate\Support\Carbon;

$born = Carbon::createFromDate(1987, 4, 23);

$noCake = Carbon::createFromDate(2014, 9, 26);
$yesCake = Carbon::createFromDate(2014, 4, 23);

$born->isBirthday($noCake); // false
$born->isBirthday($yesCake); // true
```

## Laravel Tip 💡: The "headline" Method ([⬆️](#helpers-tips-cd-))

Ever needed to convert a string to a title? Laravel ships with the "headline" method to do exactly that 🚀

```php
<?php

Str::headline('a_cool_title'); // A Cool Title

Str::headline('EmailNotificationSent'); // Email Notification Sent

// Also works with fluent strings 🔥
str('a_cool_title')->headline();
```

## Laravel Tip 💡: Sort Arrays Recursively ([⬆️](#helpers-tips-cd-))

Have you ever needed to sort an array recursively, including all its sub arrays? Laravel ships with the "sortRecursive" method to do exactly that 🚀

```php
<?php

use Illuminate\Support\Arr;
 
$array = [
    ['PHP', 'Ruby', 'JavaScript'],
    ['one' => 1, 'two' => 2, 'three' => 3],
];
 
Arr::sortRecursive($array);
 
/*
    [
        ['one' => 1, 'three' => 3, 'two' => 2],
        ['JavaScript', 'PHP', 'Ruby'],
    ]
*/

// You can also sort in a desc order
Arr::sortRecursiveDesc($array);
```

## Laravel Tip 💡: The "data_forget" Helper ([⬆️](#helpers-tips-cd-))

Have you ever needed to unset data from nested arrays? It can get messy (and ugly) quickly. Laravel ships with the "data_forget" helper to do exactly that using the dot notation 🚀

```php
<?php
 
$data = ['products' => ['desk' => ['price' => 100]]];
 
data_forget($data, 'products.desk.price'); // ['products' => ['desk' => []]]
```

## Laravel Tip 💡: The New "doesntContain" String Method ([⬆️](#helpers-tips-cd-))

Sometimes, you might need to check if a string does not contain a given value. Previously, you could negate the "contains" helper, but things just got even better with the new "doesntContain" method 🚀

```php
<?php

use Illuminate\Support\Str;

if (!Str::contains('Larvel forever', 'Laravel')) {
    // string does not contain Laravel, fix it
}

if (Str::doesntContain('Larvel forever', 'Laravel')) {
    // string does not contain Laravel, fix it
}
```

## Laravel Tip 💡: Spell Ordinal Numbers ([⬆️](#helpers-tips-cd-))

Starting from Laravel v11.34, you can now spell ordinal numbers using the newly introduced "spellOrdinal" method 🚀

```php
<?php

use Illuminate\Support\Number;
 
$position = Number::ordinal(3); // 3rd

// Now you can spell it 🔥
$position = Number::spellOrdinal(3); // third
```

## Laravel Tip 💡: The "keyBy" Method ([⬆️](#helpers-tips-cd-))

Have you ever needed to key your eloquent collection by an attribute from its items? While you can hack your way with pluck, the "keyBy" method does exactly that 🚀

```php
<?php

$collection = collect([
    ['product_id' => 'prod-100', 'name' => 'Desk'],
    ['product_id' => 'prod-200', 'name' => 'Chair'],
]);

// Instead of doing this or any manual transformation
$keyed = $collection->pluck(null, 'product_id');

// You can simply do this 🔥
$keyed = $collection->keyBy('product_id');

$keyed->all();

/*
    [
        'prod-100' => ['product_id' => 'prod-100', 'name' => 'Desk'],
        'prod-200' => ['product_id' => 'prod-200', 'name' => 'Chair'],
    ]
*/
```

## Laravel Tip 💡: The "remove" Str Method ([⬆️](#helpers-tips-cd-))

Have you ever needed to remove some characters from a text? While you can do it manually with built-in PHP functions, Laravel provides a much more readable wrapper "remove", which you can also chain with other methods 🚀

```php
<?php

use Illuminate\Support\Str;

$string = 'Peter Piper picked a peck of pickled peppers.';

// This works
str_replace('e', '', $string); // Ptr Pipr pickd a pck of pickld ppprs.

// But this reads much better 🔥 and supports case insensitive as well
Str::remove('e', $string, caseSensitive: false); // Ptr Pipr pickd a pck of pickld ppprs.

// You can also remove multiple letters at once
Str::remove(['e', 'i', 't'], $string); // Pr Ppr pckd a pck of pckld ppprs.
```

## Laravel Tip 💡: Check If a String Is a URL ([⬆️](#helpers-tips-cd-))

Have you ever needed to check if a given string is a valid URL? While you could do this manually, Laravel ships with the "isUrl" method to do exactly that. You can even take it a step further and check for various protocols 🚀

```php
<?php

use Illuminate\Support\Str;
 
Str::isUrl('http://valid-url.com', ['https', 'http']); // true
 
Str::isUrl('ftp://yourserverdomain.com'); // true

Str::isUrl('non-valid-url'); // false
```

## Laravel Tip 💡: Extract Text Between Strings ([⬆️](#helpers-tips-cd-))

Have you ever needed to extract text that is between 2 strings? Laravel ships with the "between" method to do exactly that 🚀

```php
<?php

use Illuminate\Support\Str;
 
$slice = Str::between('This is my name', 'This', 'name');
 
// ' is my '
```

## Laravel Tip 💡: Reusable Pipelines ([⬆️](#helpers-tips-cd-))

Pipelines allow you to split a large task into smaller, more manageable ones. Sometimes, you may want to use the same pipeline in different places, and it turns out Laravel allows you to define reusable pipelines out of the box 🚀

```php
<?php

use Illuminate\Contracts\Pipeline\Hub;
use Illuminate\Pipeline\Pipeline;

// In a service provider
public function boot()
{
    $this->app
        ->get(Hub::class)
        // Register a named pipeline that can be reused elsewhere
        ->pipeline('process-uploaded-image', function (Pipeline $pipeline, $image) {
            return $pipeline
                ->send($image)
                ->through([
                    ValidateImage::class,
                    Resize::class,
                    Optimize::class,
                    // ... more stages to handle the image
                ])
                ->thenReturn();
        });
}

// Anywhere you handle image uploads
Route::get('/upload-image', function (Hub $hub, Request $request) {
    $image = $request->file('image');

    $processedImage = $hub->pipe($image, 'process-uploaded-image');
});
```

## Laravel Tip 💡: Clamp Numbers ([⬆️](#helpers-tips-cd-))

Have you ever needed to keep a number within a specific range, like a rating or a computed value? While you can hack your way through with min and max, Laravel ships with an elegant helper "clamp" to do exactly that 🚀

```php
<?php

use Illuminate\Support\Number;

Number::clamp(55, min: 10, max: 50); // Above the range, so the max 50 is returned

Number::clamp(5, min: 10, max: 50); // Below the range, so the min 10 is returned

Number::clamp(20, min: 10, max: 50); // Within the range, so the original value 20 is returned
```

## Laravel Tip 💡: Select Sub-Arrays ([⬆️](#helpers-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D10.45-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

There will be times when you need to extract a sub-array from the main one, whether it's from a JSON response, your models, or whatever. While you could use "map" for that, Laravel ships with a much more elegant helper, "select", just for this 🚀

```php
<?php

use App\Models\Product;

// Instead of this 🥱
Product::all()->map(
    fn(Product $product) => collect($product)->only(['name', 'price'])->toArray()
);

// You can do this instead 🔥
Product::all()->select('name', 'price');

/**
 * Reminders:
 * - pluck() only works for a single key
 * - only() can't handle nested arrays
 */
```

## Laravel Tip 💡: Date Checks with Carbon ([⬆️](#helpers-tips-cd-))

I know you've had to check if a date has expired or is in the future at least once. Since Laravel uses Carbon under the hood, you've got access to a ton of helpers to handle all that elegantly 🚀

```php
<?php

use Illuminate\Support\Carbon;

$date = Carbon::createFromDate(2025, 7, 28);

$date->isToday();      // true
$date->isTomorrow();   // false
$date->isYesterday();  // false

$date->isWeekday();    // true
$date->isWeekend();    // false

$date->isFuture();     // false
$date->isPast();       // false

// But wait, there's more 🔥
$date->isSameDay(now());    // true
$date->isSameWeek(now());   // true
$date->isSameMonth(now());  // true
$date->isSameYear(now());   // true

// You can even specify a unit
$date->isSameUnit('year', now()); // true

// And the list goes on... 😎
```

## Laravel Tip 💡: Handle Pluralization Elegantly ([⬆️](#helpers-tips-cd-))

Did you know that besides localization, Laravel also handles pluralization out of the box? When you have messages in different plural forms, you can define them all at once and even use ranges to specify which format to use for each case 🚀

```php
<?php

// In your lang/en/messages.php
return [
    'count' => '{0} Be the first to comment|{1} One comment|[2,*] :count comments',
];

trans_choice('messages.count', 0);  // "Be the first to comment"
trans_choice('messages.count', 1);  // "One comment"
trans_choice('messages.count', 10); // "10 comments"

// Yes, you also get messages depending on the set locale 🔥
// Another bonus: No more ugly if statements 🔥
```
