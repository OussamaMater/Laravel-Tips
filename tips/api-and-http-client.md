# API & The HTTP Client Tips ([cd ..](../README.md))

- [The "withToken()" method](#laravel-tip--the-withtoken-method-️)
- [Extend the "PersonalAccessToken" model](#laravel-tip--extend-the-personalaccesstoken-model-️)
- [HTTP Client Handler Stats](#laravel-tip--http-client-handler-stats-️)
- [Without Data Wrapping](#laravel-tip--without-data-wrapping-️)
- [Collect API Responses](#laravel-tip--collect-api-responses-️)
- [A Better Content Negotiation](#laravel-tip--a-better-content-negotiation-️)
- [Get Bearer Tokens Elegantly](#laravel-tip--get-bearer-tokens-elegantly-️)
- [Retry Concurrent Requests](#laravel-tip--retry-concurrent-requests-️)
- [Send Concurrent Requests](#laravel-tip--send-concurrent-requests-️)
- [URI Templates](#laravel-tip--uri-templates-️)
- [Global Middleware for HTTP Client](#laravel-tip--global-middleware-for-http-client-️)

## Laravel Tip 💡: The "withToken()" method ([⬆️](#api--the-http-client-tips-cd-))

Did you know that the Laravel HTTP Client comes with a fluent method called "withToken()" that you can use to set bearer tokens? 🚀

```php
<?php

// The following code
Http::withHeaders([
    'Authorization' => 'Bearer eyJhbGciOiJIUz...',
]);

// Is equivalent to this
Http::withToken('eyJhbGciOiJIUz...');
```

## Laravel Tip 💡: Extend the "PersonalAccessToken" model ([⬆️](#api--the-http-client-tips-cd-))

Sanctum is a powerful package for managing API tokens. Sometimes you may wish the token model had more methods. Well, guess what? You can extend the model and register your custom one instead! 🚀

```php
<?php
use App\Models\Sanctum\PersonalAccessToken;
use Laravel\Sanctum\Sanctum;

/**
 * Bootstrap any application services.
 */
public function boot(): void
{
    // Custom token model that adds new methods such as "lastUsedAt()"
    Sanctum::usePersonalAccessTokenModel(PersonalAccessToken::class);
}

// Now this will return an instance of the custom model
$token = $request->user()->currentAccessToken();
```

## Laravel Tip 💡: HTTP Client Handler Stats ([⬆️](#api--the-http-client-tips-cd-))

The Laravel HTTP Client uses Guzzle under the hood, providing access to statistics for each request you make, including total time, download speed and much more 🚀

```php
<?php

$stats = Http::get('https://oussama-mater.tech')->handlerStats();

/*
All the statistics related to the request:
[
    "http_code" => 200
    "total_time" => 8.430478
    "speed_download" => 135.0
    "speed_upload" => 0.0
    ...
]
*/
```

## Laravel Tip 💡: Without Data Wrapping ([⬆️](#api--the-http-client-tips-cd-))

Eloquent API resources are automatically wrapped in a "data" object. Sometimes, you may want to remove this wrapping. Laravel includes the "withoutWrapping" method to do exactly that 🚀

```php
<?php

class AppServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        JsonResource::withoutWrapping();
    }
}

/*
[
    {
        "id": 1,
        "name": "Eladio Schroeder Sr.",
        "email": "therese28@example.com"
    },
    {
        "id": 2,
        "name": "Liliana Mayert",
        "email": "evandervort@example.com"
    }
]
*/
```

## Laravel Tip 💡: Collect API Responses ([⬆️](#api--the-http-client-tips-cd-))

Usually, when working with the HTTP Client, we manually collect the JSON response from the API. However, did you know that Laravel ships with the "collect" method directly on the HTTP Client? 🚀

```php
<?php

use Illuminate\Support\Facades\Http;

// Instead of this 😒
$response = Http::get('http://example.com')->json();
collect($response);

// Do this 😎
$collection = Http::get('http://example.com')->collect();
```

## Laravel Tip 💡: A Better Content Negotiation ([⬆️](#api--the-http-client-tips-cd-))

Sometimes you might have multiple response formats that you return. You can use the "getAcceptableContentTypes" method to map your response to what's best for the user 🚀

```php
<?php

request()->getAcceptableContentTypes();

// [
//     0 => "text/html",
//     1 => "application/xhtml+xml",
//     2 => "image/avif",
//     3 => "image/webp",
//     4 => "image/apng",
//     5 => "application/xml",
//     6 => "x/e",
//     7 => "application/signed-exchange",
// ];
```

## Laravel Tip 💡: Get Bearer Tokens Elegantly ([⬆️](#api--the-http-client-tips-cd-))

Building an API with Laravel? You can retrieve the bearer token using the "bearerToken" method on the request object without having to manually parse it 🚀

```php
<?php

// Instead of this 😞
$token = substr(request()->header('Authorization'), 7);

// Do this 😊
$token = request()->bearerToken();
```

## Laravel Tip 💡: Retry Concurrent Requests ([⬆️](#api--the-http-client-tips-cd-))

In Laravel versions 10 and below, retrying failed concurrent requests wasn't possible. Well, guess what? In Laravel 11, we can! 🚀

```php
<?php

use Illuminate\Http\Client\Pool;
use Illuminate\Support\Facades\Http;

$responses = Http::pool(fn (Pool $pool) => [
    $pool->as('first')->retry(2)->get('http://localhost/first'),
    $pool->as('second')->retry(2)->get('http://localhost/second'),
    $pool->as('third')->retry(2)->get('http://localhost/third'),
]);
```

## Laravel Tip 💡: Send Concurrent Requests ([⬆️](#api--the-http-client-tips-cd-))

Laravel's HTTP client wraps Guzzle, which allows you to make concurrent requests to speed things up. This is very helpful for various cases, such as health checks! 🚀

```php
<?php

use Illuminate\Http\Client\Pool;
use Illuminate\Support\Facades\Http;

$responses = Http::pool(fn (Pool $pool) => [
    $pool->get('http://localhost/first'),
    $pool->get('http://localhost/second'),
    $pool->get('http://localhost/third'),
]);

return $responses[0]->ok() &&
       $responses[1]->ok() &&
       $responses[2]->ok();
```

## Laravel Tip 💡: URI Templates ([⬆️](#api--the-http-client-tips-cd-))

Since Laravel uses Guzzle under the hood, you can use URI templates with Laravel's HTTP Client by calling the "withUrlParameters" method 🚀

```php
<?php

// This follows the URI Template specification (RFC 6570).
Http::withUrlParameters([
    'endpoint' => 'https://laravel.com',
    'page' => 'docs',
    'version' => '11.x',
    'topic' => 'validation',
])->get('{+endpoint}/{page}/{version}/{topic}');
```

## Laravel Tip 💡: Global Middleware for HTTP Client ([⬆️](#api--the-http-client-tips-cd-))

Sometimes you may want to apply global headers to all outgoing requests. For instance, a global user agent can help you identify your app's requests in other services or third-party APIs. Laravel already supports request and response middleware  to do exactly that 🚀

```php
<?php

use Illuminate\Support\Facades\Http;

Http::globalRequestMiddleware(fn ($request) => $request->withHeader(
    'User-Agent', 'Example Application/1.0'
));

Http::globalResponseMiddleware(fn ($response) => $response->withHeader(
    'X-Finished-At', now()->toDateTimeString()
));
```