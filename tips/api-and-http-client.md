# API & The HTTP Client Tips ([cd ..](../README.md))

- [Laravel Tip 💡: The "withToken()" method (⬆️)](#laravel-tip--the-withtoken-method-️)
- [Laravel Tip 💡: Extend the "PersonalAccessToken" model (⬆️)](#laravel-tip--extend-the-personalaccesstoken-model-️)
- [Laravel Tip 💡: HTTP Client Handler Stats (⬆️)](#laravel-tip--http-client-handler-stats-️)
- [Laravel Tip 💡: Without Data Wrapping (⬆️)](#laravel-tip--without-data-wrapping-️)
- [Laravel Tip 💡: Collect API Responses (⬆️)](#laravel-tip--collect-api-responses-️)
- [Laravel Tip 💡: A Better Content Negotiation (⬆️)](#laravel-tip--a-better-content-negotiation-️)
- [Laravel Tip 💡: Get Bearer Tokens Elegantly (⬆️)](#laravel-tip--get-bearer-tokens-elegantly-️)
- [Laravel Tip 💡: Retry Concurrent Requests (⬆️)](#laravel-tip--retry-concurrent-requests-️)
- [Laravel Tip 💡: Send Concurrent Requests (⬆️)](#laravel-tip--send-concurrent-requests-️)
- [Laravel Tip 💡: URI Templates (⬆️)](#laravel-tip--uri-templates-️)
- [Laravel Tip 💡: Global Middleware for HTTP Client (⬆️)](#laravel-tip--global-middleware-for-http-client-️)
- [Laravel Tip 💡: Convert Responses to Exceptions (⬆️)](#laravel-tip--convert-responses-to-exceptions-️)
- [Laravel Tip 💡: HTTP Response Status Helpers (⬆️)](#laravel-tip--http-response-status-helpers-️)
- [Laravel Tip 💡: Real-Time Download Progress (⬆️)](#laravel-tip--real-time-download-progress-️)
- [Laravel Tip 💡: The "noContent()" method (⬆️)](#laravel-tip--the-nocontent-method-️)

## Laravel Tip 💡: The "withToken()" method ([⬆️](#api--the-http-client-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D7-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Sanctum-%3E%3D2-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D8.18-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D5.5-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D8.29.0-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D5.4-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D5.4-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

Building an API with Laravel? You can retrieve the bearer token using the "bearerToken" method on the request object without having to manually parse it 🚀

```php
<?php

// Instead of this 😞
$token = substr(request()->header('Authorization'), 7);

// Do this 😊
$token = request()->bearerToken();
```

## Laravel Tip 💡: Retry Concurrent Requests ([⬆️](#api--the-http-client-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D11-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D8.37-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D9.51-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D10.14-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

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

## Laravel Tip 💡: Convert Responses to Exceptions ([⬆️](#api--the-http-client-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D9.49-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

When consuming APIs, your request might fail. While you can manually check and throw exceptions, Laravel ships with handy helpers to do exactly that 🚀

```php
<?php

// Instead of this 🥱
if ($response->clientError()) {
    throw new RequestException($response);
}

if ($response->serverError()) {
    throw new RequestException($response);
}

if ($response->failed()) {
    throw new RequestException($response);
}

// You can do this 😎
$response->throwIfClientError(); // >=400 & <500

$response->throwIfServerError(); // >= 500

// You can set an exact status
$response->throwIfStatus(403);

// Or even specify a range 🔥
$response->throwIfStatus(fn(int $status) => $status >= 400);
```

## Laravel Tip 💡: HTTP Response Status Helpers ([⬆️](#api--the-http-client-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D9.49-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

When making API requests, you often need to check the response status code. While you can do this manually, Laravel provides wrappers for almost all status codes, which you can use for elegant and readable checks 🚀

```php
<?php

use Illuminate\Support\Facades\Http;

$response = Http::get('https://blog.oussama-mater.tech');

// Instead of checking the status manually 🥱
$response->status() === 404;

// You can do this 🔥
$response->notFound(); // status code 404
$response->tooManyRequests(); // status code 429
$response->forbidden(); // status code 403
$response->unauthorized(); // status code 401
$response->unprocessableContent(); // status code 422
$response->serverError(); // status code >= 500
$response->clientError(); // status code >= 400 && <500
```

## Laravel Tip 💡: Real-Time Download Progress ([⬆️](#api--the-http-client-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D7-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

If you ever need to download a file in your Laravel app, consider using Guzzle's "progress" option. It gives you real-time updates on the download, which you can broadcast to your UI, display in the console, or handle however you like 🚀

```php
<?php

use Illuminate\Support\Facades\Http;

Http::withToken('an-api-token')
    ->get('https://api.example.com/plugins/some-theme')
    ->timeout(30)
    ->withOptions([
        'sink' => storage_path('plugins/some-theme.zip'),
        'progress' => function ($downloadTotal, $downloadedBytes) {
            // You can emit an event to the frontend for real-time updates,
            event(new PluginDownloadProgress($downloadedBytes, $downloadTotal));
            // Or update a progress bar in a console command, etc..
        }
    ]);
```

## Laravel Tip 💡: The "noContent()" method ([⬆️](#api--the-http-client-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D5.2-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

When building RESTful APIs, deleted resources should typically return a 204 No Content response. While you can return the response manually, Laravel already ships with the handy "noContent()" method for exactly this 🚀

```php
<?php

// Instead of this 😴
return response('', 204);

// Do this 😎
return response()->noContent();
```
