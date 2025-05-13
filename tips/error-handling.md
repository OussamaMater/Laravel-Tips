# Error Handling Tips ([cd ..](../README.md))

- [Mapping Exceptions via Handler](#laravel-tip--mapping-exceptions-via-handler-️)
- [Mapping Exception via Custom Exception Classes](#laravel-tip--mapping-exception-via-custom-exception-classes-️)
- [Report Internal Exceptions](#laravel-tip--report-internal-exceptions-️)
- [Skip Exception Reporting](#laravel-tip--skip-exception-reporting-️)
- [Better Custom Exceptions](#php-tip--better-custom-exceptions-️)

## Laravel Tip 💡: Mapping Exceptions via Handler ([⬆️](#error-handling-tips-cd-))

>[!NOTE]
>Since Laravel 11, the directory structure has changed, and exception handling is now managed in `app.php`. This tip applies to Laravel versions earlier than 11.

Did you know that you can map exceptions to other exceptions? This is helpful when you have custom exceptions that you'd like to be handled like internal ones, or when you want to wrap third-party exceptions and map them to your own 🚀

```php
<?php

namespace App\Exceptions;

use App\Exceptions\MyCustomException;
use Illuminate\Database\Eloquent\ModelNotFoundException;
use Illuminate\Foundation\Exceptions\Handler as ExceptionHandler;

class Handler extends ExceptionHandler
{
    // MyCustomException is now handled as if it were ModelNotFoundException
    protected $exceptionMap = [
        MyCustomException::class => ModelNotFoundException::class,
    ];
}
```

## Laravel Tip 💡: Mapping Exception via Custom Exception Classes ([⬆️](#error-handling-tips-cd-))

>[!NOTE]
>Since Laravel 11, the directory structure has changed, and exception handling is now managed in `app.php`. This tip applies to Laravel versions earlier than 11.

When defining a custom exception, there is a secret way to map the exception to another one, and this is done by defining the `getInnerException` method 🚀

Curious about how the mapping is done? Take a look at `Illuminate\Foundation\Exceptions\Handler::mapException()`

```php
<?php

namespace App\Exceptions;

use Exception;
use Throwable;
use Illuminate\Database\Eloquent\ModelNotFoundException;

class MyCustomException extends Exception
{
    // MyCustomException is now handled as if it were ModelNotFoundException
    public function getInnerException(): Throwable
    {
        return new ModelNotFoundException;
    }
}
```

## Laravel Tip 💡: Report Internal Exceptions ([⬆️](#error-handling-tips-cd-))

>[!NOTE]
>Since Laravel 11, the directory structure has changed, and exception handling is now managed in `app.php`. This tip applies to Laravel versions earlier than 11.

Sometimes, you just wish to report internal exceptions. For instance, if you want to know exactly where that 404 error is being thrown, you can do so by overriding the `internalDontReport` array 🚀

```php
<?php

namespace App\Exceptions;

use Illuminate\Foundation\Exceptions\Handler as ExceptionHandler;

// The ModelNotFoundException exception will now be reported
class Handler extends ExceptionHandler
{
    protected $internalDontReport = [
        AuthenticationException::class,
        AuthorizationException::class,
        BackedEnumCaseNotFoundException::class,
        HttpException::class,
        HttpResponseException::class,
        //ModelNotFoundException::class,
        MultipleRecordsFoundException::class,
        RecordsNotFoundException::class,
        SuspiciousOperationException::class,
        TokenMismatchException::class,
        ValidationException::class,
    ];
}
```

## Laravel Tip 💡: Skip Exception Reporting ([⬆️](#error-handling-tips-cd-))

There are some exceptions that you may not want to report to your monitoring tool. While you could manually register them in "app.php", you can just mark the exception with the "ShouldntReport" interface 🚀

```php
<?php

namespace App\Exceptions;

use Exception;
use Illuminate\Contracts\Debug\ShouldntReport;

class PodcastProcessingException extends Exception implements ShouldntReport
{
    //
}
```

## PHP Tip 💡: Better Custom Exceptions ([⬆️](#error-handling-tips-cd-))

Do you use custom exceptions in your codebase and end up with multiple empty classes? You can group all related exceptions into a single class and use static methods to create english-like code that immediately tells you what went wrong 🚀

```php
<?php

namespace App\Exceptions;

use Exception;

final class CouldNotStartAbTest extends Exception
{
    public static function testDoesNotHaveEnoughVariants(string $abTestName): static
    {
        return new static(
            "Could not start the test '{$abTestName}'. At least 2 variants are required."
        );
    }

    // Group all related exceptions here
}

// Instead of hardcoding the message
throw new Exception('Could not start the test new-navbar. At least 2 variants are required.');

// Or creating a separate custom exception for each error, which is just an empty class
throw new NotEnoughAbTestVariantsException();

// You can group all related exceptions into a single class, 
// which makes the code more readable and maintainable
throw CouldNotStartAbTest::testDoesNotHaveEnoughVariants('new-navbar');
```
