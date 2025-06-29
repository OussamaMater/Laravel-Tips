# Testing Tips ([cd ..](../README.md))

- [Prevent Stray Requests](#laravel-tip--prevent-stray-requests-️)
- [Faker Formatters](#laravel-tip--faker-formatters-️)
- [Optional Faker Values](#laravel-tip--optional-faker-values-️)
- [Test Queue/Job Interactions](#laravel-tip--test-queuejob-interactions-️)
- [Factory Sequences](#laravel-tip--factory-sequences-️)
- [Make Use Of Factory States](#laravel-tip--make-use-of-factory-states-️)
- [Faker Random Element](#laravel-tip--faker-random-element-️)
- [Pest Higher Order Expectations](#pest-tip--higher-order-expectations-️)
- [Pest Intercept Exceptions](#pest-tip--intercept-exceptions-️)
- [Recycle Existing Models](#laravel-tip--recycle-existing-models-️)
- [Catch Flaky Tests](#laravel-tip--catch-flaky-tests-️)
- [Assert Model Missing](#laravel-tip--assert-model-missing-️)
- [Faker "valid()" Modifier](#laravel-tip--faker-valid-modifier-️)
- [Freeze Time](#laravel-tip--freeze-time-️)
- [Generate Fake User Agents](#laravel-tip--generate-fake-user-agents-️)
- [Time Travel in Your Tests](#laravel-tip--time-travel-in-your-tests-️)
- [Shape Your Strings](#laravel-tip--shape-your-strings-️)
- [Assert JSON Fragments](#laravel-tip--assert-json-fragments-️)
- [Magic Factories Methods](#laravel-tip--magic-factories-methods-️)
- [Generate Fake Credit Card Numbers](#laravel-tip--generate-fake-credit-card-numbers-️)
- [Generate Currency Code](#laravel-tip--generate-currency-code-️)
- [Lazily Refresh Your Database](#laravel-tip--lazily-refresh-your-database-️)
- [Run Seeders During Tests](#laravel-tip--run-seeders-during-tests-️)
- [Faker's "randomDigitNot()"](#laravel-tip--fakers-randomdigitnot-️)
- [Use the "set" Method in Factories](#laravel-tip--use-the-set-method-in-factories-️)
- [Generate Fake Credit Card Details](#laravel-tip--generate-fake-credit-card-details-️)
- [Autocompletion in PestPHP](#laravel-tip--autocompletion-in-pestphp-️)
- [Record API Responses as Fixtures](#laravel-tip--record-api-responses-as-fixtures-️)

## Laravel Tip 💡: Prevent Stray Requests ([⬆️](#testing-tips-cd-))

Did you know that Laravel ships with the "preventStrayRequests()" method to avoid making actual requests during testing? This is handy not only for third-party APIs but also for local APIs. While your tests may pass locally because the entire environment is up and running, they could fail in the CI pipeline. This happens because, in the CI pipeline, typically only the service you are testing is active, so making actual requests to unavailable APIs will cause your suite to fail.

```php
<?php

use Illuminate\Support\Facades\Http;

// Define in your setUp()
Http::preventStrayRequests();

// Now in your tests
Http::fake([
    'example.com/*' => Http::response('ok'),
]);

// An "ok" response is returned ...
Http::get('https://example.com/users');

// An exception is thrown ...
Http::get('https://oussama-mater.tech');
```

## Laravel Tip 💡: Faker Formatters ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP for generating fake data, you can employ both, "numerify" and "bothify", to generate data in a specific pattern 🚀

```php
<?php

$faker = Faker\Factory::create();

// 2067-7317-8584-7068
$creditCardNumber = $faker->numerify('####-####-####-####');

// TRK-cwq-546-shx
$trackingNumber = $faker->bothify('TRK-???-###-???');
```

## Laravel Tip 💡: Optional Faker Values ([⬆️](#testing-tips-cd-))

If you have optional columns in your table that you want to seed randomly, FakerPHP (what Laravel uses under the hood) allows for optional values out of the box 🚀

```php
<?php

fake()->optional()->randomDigit(); // a random digit, but also null sometimes

fake()->optional($weight = 0.1)->randomDigit(); // 90% chance of NULL
fake()->optional($weight = 0.9)->randomDigit(); // 10% chance of NULL

fake()->optional($weight = 10)->randomDigit; // 90% chance of NULL
fake()->optional($weight = 100)->randomDigit; // 0% chance of NULL

fake()->optional($weight = 0.5, $default = false)->randomDigit(); // 50% chance of FALSE
fake()->optional($weight = 0.9, $default = 'abc')->word(); // 10% chance of 'abc'
```

## Laravel Tip 💡: Test Queue/Job Interactions ([⬆️](#testing-tips-cd-))

Laravel 11 has introduced a new way of testing failed, released or deleted jobs, which was a challenging in previous versions! You can now simply chain "withFakeQueueInteractions" on your job and assert one of the mentioned actions 🚀

```php
<?php

use App\Jobs\ProcessPodcast;

$job = (new ProcessPodcast)->withFakeQueueInteractions();

$job->handle();

$job->assertReleased(delay: 30);
$job->assertDeleted();
$job->assertFailed();
```

## Laravel Tip 💡: Factory Sequences ([⬆️](#testing-tips-cd-))

Did you know that Laravel allows you to define sequences when using factories? This makes setting up complex tests a breeze 🚀

```php
<?php

$users = User::factory()
    ->count(2)
    ->sequence(
        ['name' => 'First User'],
        ['name' => 'Second User'],
    )
    ->create();
```

## Laravel Tip 💡: Make Use Of Factory States ([⬆️](#testing-tips-cd-))

Did you know that Laravel factories allow you to define states? You can use multiple states to describe the object and apply discrete modifications to it. This also makes the code more readable! 🚀

```php
<?php

use Illuminate\Database\Eloquent\Factories\Factory;

// Define the state in the user factory
public function suspended(): Factory
{
    return $this->state(function (array $attributes) {
        return [
            'account_status' => Status::SUSPENDED,
        ];
    });
}

// Now you can use it like so
$user = User::factory()->suspended()->create();
```

## Laravel Tip 💡: Faker Random Element ([⬆️](#testing-tips-cd-))

Sometimes, when defining factories, you may want to pick a random element from an array. Since Laravel uses FakerPHP under the hood, you can do this by calling the "randomElement" method 🚀

```php
// Get a random subscription type
$random = fake()->randomElement(['basic', 'premium']);

// Get a random letter
$random = fake()->randomElement(['a', 'b', 'c']);
```

## Pest Tip 💡: Higher Order Expectations ([⬆️](#testing-tips-cd-))

Did you know that [@pestphp](https://twitter.com/pestphp) ships with "Higher Order Expectations"? It allows you to perform expectations on the properties and/or methods of the given object. This results in a much cleaner code

```php
<?php

// Instead of this 😫
expect($user->name)->toBe('John');
expect($user->country)->toBe('us');
expect($user->isAdmin())->toBeFalse();

// Do this 😎
expect($user)
    ->name->toBe('John')
    ->country->toBe('us')
    ->isAdmin()->toBeFalse();
```

## Pest Tip 💡: Intercept Exceptions ([⬆️](#testing-tips-cd-))

One of the cool features in Pest is "intercepting" exceptions. You can override built-in expectations with your own implementation and still fallback to the default behavior for regular cases 🚀

```php
<?php

use Illuminate\Database\Eloquent\Model;
use App\Models\User;

// In your tests/Expectations.php file
expect()->intercept('toBe', Model::class, function (Model $expected) {
    expect($this->value->is($expected))
    // You can also set a custom message
    ->toBeTrue(message: 'Failed asserting that both models are the same.');
});

// Now you can use it in your tests 😎
test('models', function () {
    $user = User::find(1);
    $sameUser = User::find(1);
    
    expect($user)->toBe($sameUser);
});

// It will still work as it used to 👍
test('old expectation', function () {
    expect('hello-world')->toBe('hello-world');
});
```

## Laravel Tip 💡: Recycle Existing Models ([⬆️](#testing-tips-cd-))

When defining factories, you may want to use a single model for all the relationships instead of creating a new one for each of them. Laravel ships with a cool method "recycle" to do exactly that 🚀

```php
<?php

$airlines = Airline::factory()->count(3)->create();

// Only 3 airlines will be used for the 100 tickets
Ticket::factory()
    ->count(100)
    ->recycle($airlines) // You can pass a single one
    ->create();
```

## Laravel Tip 💡: Catch Flaky Tests ([⬆️](#testing-tips-cd-))

Sometimes when you write tests, you might end up with some flaky ones that are just unstable; those tests fail once in a thousand. PestPHP comes with a really cool helper, "repeat," to catch those 🚀

```php
<?php

it('can repeat a test', function() {
    $result = /** Some code that may be unstable */;

    expect($result)->toBeTrue();
})->repeat(100); // Repeat the test 100 times
```

## Laravel Tip 💡: Assert Model Missing ([⬆️](#testing-tips-cd-))

When writing tests, we often use `assertDatabaseMissing` to check whether a model has been deleted. Did you know that Laravel ships with a cool helper called `assertModelMissing` to do exactly that? 🚀

```php
<?php

use App\Models\User;

$user = User::factory()->create();

$user->delete();

// Instead of this 🥱
$this->assertDatabaseMissing('users', [
    'email' => $user->email,
]);

// You can do this 😎
$this->assertModelMissing($user);
```

## Laravel Tip 💡: Faker "valid()" Modifier ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP under the hood, you can use the "valid()" modifier to ensure that the generated fake data follows certain rules 🚀

```php
<?php

// This will only generate even numbers
$evenNumber = fake()->valid(fn (int $digit) => $digit % 2 === 0)->randomDigit();
```

## Laravel Tip 💡: Freeze Time ([⬆️](#testing-tips-cd-))

When writing tests, we sometimes need to "freeze" time to make assertions. Laravel provides an elegant method "freezeTime" to do exactly that 🚀

```php
<?php

// Instead of this 🥱
Carbon::setTestNow(now());

// Do this 😎
$this->freezeTime();
```

## Laravel Tip 💡: Generate Fake User Agents ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP under the hood, you can generate fake user agents for your tests. 🚀

```php
<?php

echo fake()->userAgent();
// Mozilla/5.0 (iPad; CPU OS 8_0_2 like Mac OS X; sl-SI) AppleWebKit/532.22.4 (KHTML, like Gecko) Version/3.0.5 Mobile/8B114 Safari/6532.22.4

echo fake()->chrome();
// Mozilla/5.0 (X11; Linux i686) AppleWebKit/5352 (KHTML, like Gecko) Chrome/38.0.899.0 Mobile Safari/5352

echo fake()->firefox();
// Mozilla/5.0 (Windows 98; Win 9x 4.90; sl-SI; rv:1.9.1.20) Gecko/20220314 Firefox/35.0

echo fake()->safari();
// Mozilla/5.0 (Windows; U; Windows NT 5.1) AppleWebKit/531.4.3 (KHTML, like Gecko) Version/5.1 Safari/531.4.3

echo fake()->opera();
// Opera/8.71 (Windows NT 4.0; nl-NL) Presto/2.11.217 Version/12.00

echo fake()->internetExplorer();
// Mozilla/5.0 (compatible; MSIE 5.0; Windows NT 5.1; Trident/4.0)

echo fake()->msedge();
// Mozilla/5.0 (iPhone; CPU iPhone OS 13_1 like Mac OS X) AppleWebKit/535.2 (KHTML, like Gecko) Version/15.0 EdgiOS/98.01106.3 Mobile/15E148 Safari/535.2
```

## Laravel Tip 💡: Time Travel in Your Tests ([⬆️](#testing-tips-cd-))

Did you know that Laravel comes with a cool time helper that allows you to travel into the future or the past in your tests? 🚀

```php
<?php

// Travel into the future...
$this->travel(5)->milliseconds(); // Travel 5 milliseconds into the future
$this->travel(5)->seconds();
$this->travel(5)->minutes();
$this->travel(5)->hours();
$this->travel(5)->days();
$this->travel(5)->weeks();
$this->travel(5)->years();

// Travel into the past...
$this->travel(-5)->hours(); // Travel 5 years into the past

// Travel to an explicit time...
$this->travelTo(now()->subHours(6));

// Return back to the present time...
$this->travelBack();
```

## Laravel Tip 💡: Shape Your Strings ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP for generating fake data, you can use "lexify" to generate strings in a specific pattern 🚀

```php
<?php

fake()->lexify(); // 'sakh', 'qwei', 'adsj'

fake()->lexify('id-????'); // 'id-xoqe', 'id-pqpq', 'id-zpeu'
```

## Laravel Tip 💡: Assert JSON Fragments ([⬆️](#testing-tips-cd-))

When testing APIs, we often need to check if the response contains a specific key with the expected data. Laravel ships with the "assertJsonFragment" to do exactly that 🚀

```php
<?php

Route::get('/users', function () {
    return [
        'users' => [
            [
                'name' => 'John Doe',
            ],
        ],
    ];
});

$response->assertJsonFragment(['name' => 'John Doe']);
```

## Laravel Tip 💡: Magic Factories Methods ([⬆️](#testing-tips-cd-))

We use factories a lot. Did you know about the for[Relation] and has[Relation] magic methods? You just need to make sure you have the relationship set up in your model and you are set 🚀

```php
<?php

// You need to have User and Post factories.
$user = User::factory()
    // The User model has a hasMany "posts" relationship.
    ->hasPosts(3)
    ->create();

$posts = Post::factory()
    ->count(3)
    // The Post model has a belongsTo "user" relationship.
    // The array is optional. Use it to override an attribute if needed.
    ->forUser([
        'name' => 'John Doe',
    ])
    ->create();
```

## Laravel Tip 💡: Generate Fake Credit Card Numbers ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP under the hood, you can generate fake credit card numbers for your tests 🚀

```php
<?php

fake()->creditCardNumber(); // '5151791946409422'

fake()->creditCardNumber('Visa'); // 4147628831960830

fake()->creditCardNumber('Visa', formatted: true); // 4147-6288-3196-0830

// You can even generate card types
fake()->creditCardType(); // MasterCard
```

## Laravel Tip 💡: Generate Currency Code ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP under the hood, you can generate random currency codes. This is really useful for fintech apps 🚀

```php
<?php

fake()->currencyCode();
// 'TND', 'AED', 'SAR', 'KZT'
```

## Laravel Tip 💡: Lazily Refresh Your Database ([⬆️](#testing-tips-cd-))

We often need to refresh the database when testing the code. In such cases, you can lazily refresh your database, so migrations are run only when you are hitting the db. This will help speed up your tests 🚀

```php
<?php

namespace Tests\Feature;

use Illuminate\Foundation\Testing\RefreshDatabase;
use Illuminate\Foundation\Testing\LazilyRefreshDatabase;
use Tests\TestCase;

class ExampleTest extends TestCase
{
    use RefreshDatabase;
    // use LazilyRefreshDatabase;

    public function test_basic_example(): void
    {
        $response = $this->get('/');

        // ...
    }
}
```

## Laravel Tip 💡: Run Seeders During Tests ([⬆️](#testing-tips-cd-))

Did you know you can run database seeders within your tests? This allows you to keep your tests clean by moving setup logic to seeders 🚀

```php
<?php

use function Pest\Laravel\seed;

uses(LazilyRefreshDatabase::class);

// For feature tests with PHPUnit, you can simply call $this->seed()
test('orders can be created', function () {
    // Run the DatabaseSeeder ...
    seed();

    // Run a specific seeder ...
    seed(OrderStatusSeeder::class);

    // Run an array of specific seeders ...
    seed([
        OrderStatusSeeder::class,
        TransactionStatusSeeder::class,
    ]);
});
```

## Laravel Tip 💡: Faker's "randomDigitNot()" ([⬆️](#testing-tips-cd-))

When defining factories, you may sometimes need to generate a random digit while excluding a specific one. Since Laravel uses FakerPHP under the hood, you can use "randomDigitNot" to do exactly that 🚀

```php
<?php

// This will return a digit from 0 to 9
fake()->randomDigit();

// You can also exclude a digit
fake()->randomDigitNot(3); // This will return any digit from 0 to 9, except 3
```

## Laravel Tip 💡: Use the "set" Method in Factories ([⬆️](#testing-tips-cd-))

Sometimes you may want to override or pass a single attribute to your factory. While you can pass a whole array for that, you can use the "set" method, which does exactly that 🚀

```php
<?php

// Rather than passing an array for just a single attribute
User::factory()->create(['email' => 'john@example.com']);

// You can use set() 🔥 Plus, It's more readable 😊
User::factory()
    ->set('email', 'john@example.com')
    ->create();
```

## Laravel Tip 💡: Generate Fake Credit Card Details ([⬆️](#testing-tips-cd-))

Since Laravel uses FakerPHP to generate fake data, you can use the "creditCardDetails" method to generate fake credit cards for your tests 🚀

```php
<?php

fake()->creditCardDetails();

// [
//   "type" => "Visa Retired"
//   "number" => "4485338826091"
//   "name" => "Ron Effertz"
//   "expirationDate" => "07/25"
// ]

// If you want to generate potentially expired cards you can pass false
fake()->creditCardDetails(valid: false);

// [
//   "type" => "MasterCard"
//   "number" => "5125073907573220"
//   "name" => "Dr. Thelma Koelpin PhD"
//   "expirationDate" => "08/22"
// ]
```

## Laravel Tip 💡: Autocompletion in PestPHP ([⬆️](#testing-tips-cd-))

When writing Pest tests, you will likely use "$this", which is not good for IDE autocompletion and may require adding a PHPDoc. To avoid this, use the "test()" helper instead, which returns the current Test Case instance 🚀

```php
<?php

test('the array has the specified key', function () {
    $array = [
        'name' => 'John Doe',
        'email' => 'john@example.com',
    ];

    // No autocompletion 😞
    $this->assertArrayHasKey('email', $array);

    // autocompletion works perfectly fine, and the IDE is happy 🔥
    test()->assertArrayHasKey('email', $array);
});
```

## Laravel Tip 💡: Record API Responses as Fixtures ([⬆️](#testing-tips-cd-))

If you are testing your API integrations (which you should) you are probably using the "fake()" method. To quickly prepare a stub for testing, you can use the "sink()" method to save the response into a fixture 🚀

```php
<?php

use Illuminate\Support\Facades\Http;
use Illuminate\Support\Facades\File;

// First, define the path where you want to save the API response
$path = base_path('tests/Fixtures/also-asked-post-search.json');

Http::baseUrl(config('services.alsoasked.api_url'))
    ->withHeader('X-Api-Key', config('services.alsoasked.api_key'))
    ->throw()
    ->sink($path) // sink() will save the response directly to the specified path
    ->post('search', [
        // ...
    ]);

// Now you can use the saved API response for testing 🔥
Http::fake([
    config('services.alsoasked.api_url') . 'search' => File::json($path),
]);
```
