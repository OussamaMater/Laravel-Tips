# Routing & Requests Tips ([cd ..](../README.md))

- [Model Binding in Form Requests](#laravel-tip--model-binding-in-form-requests-️)
- [Route Absolute and Relative Path](#laravel-tip--route-absolute-and-relative-path-️)
- [Customizing Missing Model Behavior](#laravel-tip--customizing-missing-model-behavior-️)
- [Custom Route Model Binding Resolution](#laravel-tip--custom-route-model-binding-resolution-️)
- [Group Resource Controllers](#laravel-tip--group-resource-controllers-️)
- [Retrieve Soft Deleted Models](#laravel-tip--retrieve-soft-deleted-models-️)
- [Redirect with URL Fragments](#laravel-tip--redirect-with-url-fragments-️)
- [Redirect Away](#laravel-tip--redirect-away-️)
- [View Routes](#laravel-tip--view-routes-️)
- [Singleton Routes](#laravel-tip--singleton-routes-️)
- [Cache Headers On The Fly](#laravel-tip--cache-headers-on-the-fly-️)
- [The "to\_route" Method](#laravel-tip--the-to_route-method-️)
- [Exclude Middleware](#laravel-tip--exclude-middleware-️)
- [Customize the Redirect Location](#laravel-tip--customize-the-redirect-location-️)
- [Laravel's Signed Routes](#laravel-tip--laravels-signed-routes-️)
- [The "expectsJson" Method](#laravel-tip--the-expectsjson-method-️)
- [Better Checks For Input Presence](#laravel-tip--better-checks-for-input-presence-️)
- [The "mergeIfMissing" Method](#laravel-tip--the-mergeifmissing-method-️)
- [The "hasHeader" Method](#laravel-tip--the-hasheader-method-️)
- [Force HTTPS for URLs](#laravel-tip--force-https-for-urls-️)
- [The New "RouteParameter" Attribute](#laravel-tip--the-new-routeparameter-attribute-️)
- [Disable Scope Bindings](#laravel-tip--disable-scope-bindings-️)
- [Detect User Language](#laravel-tip--detect-user-language-️)

## Laravel Tip 💡: Model Binding in Form Requests ([⬆️](#routing--requests-tips-cd-))

Route Model Binding allows you to inject the model instances directly into your routes. It is usually used within a controller, but did you know you could also access the model instance in your Form Request?

```php
<?php

// Route definition
Route::put('/post/{post}', [PostsController::class, 'create']);

  
// Form Request defintion
class PostController extends FormRequest
{
    public function authorize(): bool
    {
        // The post instance, if found
        return $this->user()->can('create', $this->route('post'));
    }

    public function rules(): array
    {
        return [
            // ...
        ];
    }
}
```

## Laravel Tip 💡: Route Absolute and Relative Path ([⬆️](#routing--requests-tips-cd-))

In Laravel, the route() helper is used to generate paths for named routes; by default, it generates the absolute path. Did you know that if you pass False as your third parameter, it will generate a relative path? Now you do 🚀

```php
<?php

route('tips', $tip->id); // https://oussama-mater.tech/tips/1

route('tips', $tip->id, false); // /tips/1
```

## Laravel Tip 💡: Customizing Missing Model Behavior ([⬆️](#routing--requests-tips-cd-))

Did you know that Laravel provides the "missing()" method to customize the default route model binding behavior when a model is not found? 🚀

```php
<?php

use App\Http\Controllers\LocationsController;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Redirect;

Route::get('/locations/{location:slug}', [LocationsController::class, 'show'])
    ->name('locations.view')
    ->missing(function (Request $request) {
        return Redirect::route('locations.index');
    });
```

## Laravel Tip 💡: Custom Route Model Binding Resolution ([⬆️](#routing--requests-tips-cd-))

Laravel's route model binding is a powerful feature that automatically injects your model into your controller. By default, it uses the ID to fetch the instance. If you wish, you can implement custom logic for resolution by defining "resolveRouteBinding" 🚀

```php
<?php

// In your model
class Post extends Model
{
    public function resolveRouteBinding($value, $field = null)
    {
        return $this
            ->where('slug', $value)
            ->orWhere('uuid', $value)
            ->firstOrFail();
    }
}

/*
Now both these will work
/post/resolve-route-binding-is-cool
/post/638fd97b-4a96-469e-b497-9e553f13c8ef
*/
Route::get('/post/{post}', fn (Post $post) => $post);
```

## Laravel Tip 💡: Group Resource Controllers ([⬆️](#routing--requests-tips-cd-))

Did you know that you can group resource controllers using the "resources()" method? It makes routing even cleaner! 🚀

```php
<?php

use App\Http\Controllers\PostsController;
use App\Http\Controllers\PhotosController;

// Instead of this
Route::resource('posts', PostsController::class);
Route::resource('photos', PhotosController::class);

// Do this
Route::resources([
    'posts' => PostsController::class,
    'photos' => PhotosController::class,
]);
```

## Laravel Tip 💡: Retrieve Soft Deleted Models ([⬆️](#routing--requests-tips-cd-))

When using Laravel Model Binding, you may wish to include the soft deleted models as well. Luckily, Laravel comes with a handy routing method called "withTrashed" to do exactly that 🚀

```php
<?php

use App\Models\User;

// Now soft-deleted users will be included.
Route::get('/users/{user}', function (User $user) {
    return $user->email;
})->withTrashed();
```

## Laravel Tip 💡: Redirect with URL Fragments ([⬆️](#routing--requests-tips-cd-))

Did you know that Laravel comes with the "withFragment" method, which allows you to add a URI fragment when redirecting? 🚀

```php
<?php

return redirect()
    ->back()
    ->withFragment('testimonials');
    // exmaple.com/#testimonials

return redirect()
    ->route('product.show')
    ->withFragment('reviews');
    // exmaple.com/product/1#reviews
```

## Laravel Tip 💡: Redirect Away ([⬆️](#routing--requests-tips-cd-))

Sometimes, you may want to redirect your users away from your Laravel application. Luckily, there is a helper method called "away" that allows you to do exactly that 🚀

```php
<?php

redirect()->away('https://blog.oussama-mater.tech');
```

## Laravel Tip 💡: View Routes ([⬆️](#routing--requests-tips-cd-))

Did you know that Laravel ships with the "view" method, which allows you to render a view directly without having to define a closure? It's much more elegant! 🚀

```php
<?php

use Illuminate\Support\Facades\Route;

// Instead of this 🥱
Route::get('/welcome', function () {
    return view('welcome', ['foo' => 'bar']);
});

// You can do this 😎
Route::view('/welcome', 'welcome', ['foo' => 'bar']);
```

## Laravel Tip 💡: Singleton Routes ([⬆️](#routing--requests-tips-cd-))

Sometimes you may need singleton resources that can't be created but only shown or edited, like a user profile, for example. Laravel ships with a singleton helper to allow you to define these routes 🚀

```php
// Image 4: tip-114.php
<?php

use App\Http\Controllers\ProfileController;
use Illuminate\Support\Facades\Route;

Route::singleton('profile', ProfileController::class);
/*
This will result in the following routes:
GET         /profile
GET         /profile/edit
PUT/PATCH   /profile
*/
```

## Laravel Tip 💡: Cache Headers On The Fly ([⬆️](#routing--requests-tips-cd-))

Did you know that Laravel ships with a middleware "SetCacheHeaders", which you can use to set cache headers, such as "max_age" and "etag"? 🚀

```php
<?php

Route::middleware('cache.headers:public;max_age=2628000;etag')->group(function () {
    Route::get('/privacy', function () {
        // ...
    });

    Route::get('/terms', function () {
        // ...
    });
});
```

## Laravel Tip 💡: The "to_route" Method ([⬆️](#routing--requests-tips-cd-))

We often redirect our users to specific routes using the "redirect()" method. Did you know there is a shorter and more expressive method called "to_route"? 🚀

```php
<?php

// Instead of this 🥱
return redirect()->route('profile');

// You can do this 😎
return to_route('profile');
```

## Laravel Tip 💡: Exclude Middleware ([⬆️](#routing--requests-tips-cd-))

Sometimes you may need to exclude a middleware from a specific route. You can do this using the "withoutMiddleware()" method 🚀

```php
<?php

use App\Http\Middleware\EnsureTokenIsValid;

Route::middleware([EnsureTokenIsValid::class])->group(function () {
    Route::get('/', function () {
        // ...
    });

    Route::get('/profile', function () {
        // ...
    })->withoutMiddleware([EnsureTokenIsValid::class]); // Excludes the middleware
});
```

## Laravel Tip 💡: Customize the Redirect Location ([⬆️](#routing--requests-tips-cd-))

We often use form requests for validation. Did you know you can customize the redirect location upon failure? You are never limited to redirecting users back to the previous page 🚀

```php
<?php

// You can use a path
protected $redirect = '/dashboard';

// Or named routes
protected $redirectRoute = 'dashboard';

// Or even use actions
protected $redirectAction = [DashboardController::class, 'index'];
```

## Laravel Tip 💡: Laravel's Signed Routes ([⬆️](#routing--requests-tips-cd-))

A reminder that Laravel ships with signed routes. They are perfect for magic login links, temporary access, and one-time actions like unsubscribing users, all in a safe way by making sure the URL isn't tampered with 🚀

```php
<?php

use Illuminate\Support\Facades\URL;

// This will generate a signed route with an absolute path
URL::signedRoute('unsubscribe', ['user' => 1]);
// http://local.test/unsubscribe?user=1&signature=753c19...6d18baa59c3b5851

// You can choose to generate a relative path instead
URL::signedRoute('unsubscribe', ['user' => 1], absolute: false);
// unsubscribe?user=1&signature=45cb85167c31085...05641509acb600

// You can also make it temporary
URL::temporarySignedRoute(
    'unsubscribe', now()->addMinutes(30), ['user' => 1], absolute: false
);
// unsubscribe?expires=1727640587&user=1&signature=f71fa139fe2...515fe111a8
```

## Laravel Tip 💡: The "expectsJson" Method ([⬆️](#routing--requests-tips-cd-))

If you have multiple clients and some of them only expect JSON, instead of manually checking the Accept header, you can use Laravel's built-in "expectsJson" method 🚀

```php
<?php

// True when the "Accept: application/json" header is present
if ($request->expectsJson()) {
    // ...
}
```

## Laravel Tip 💡: Better Checks For Input Presence ([⬆️](#routing--requests-tips-cd-))

We often need to check if a request contains certain values. Did you know that Laravel ships with two cool methods, "has" and "hasAny", to perform these checks elegantly? 🚀

```php
<?php

// True if ALL of the values are present
if ($request->has(['name', 'email'])) {
    //
}

// True if ANY of the values are present
if ($request->hasAny(['name', 'email'])) {
    //
}
```

## Laravel Tip 💡: The "mergeIfMissing" Method ([⬆️](#routing--requests-tips-cd-))

Sometimes you may want to add additional input to the current request. While you can merge it manually, Laravel already ships with the "mergeIfMissing" method to do exactly that 🚀

```php
<?php

$request->mergeIfMissing(['votes' => 0]);
```

## Laravel Tip 💡: The "hasHeader" Method ([⬆️](#routing--requests-tips-cd-))

Have you ever needed to check for a header? While you can do it manually, Laravel ships with the "hasHeader" method to do exactly that 🚀

```php
<?php
 
if ($request->hasHeader('X-Header-Name')) {
    // ...
}
```

## Laravel Tip 💡: Force HTTPS for URLs ([⬆️](#routing--requests-tips-cd-))

Since Laravel v11.31, you can enforce HTTPS for all generated URLs without needing the HTTPS schema specified in the request 🚀

```php
<?php

use Illuminate\Support\Facades\URL;

URL::forceHttps(app()->isProduction());
```

## Laravel Tip 💡: The New "RouteParameter" Attribute ([⬆️](#routing--requests-tips-cd-))

Laravel v11.28 introduced a new attribute `RouteParameter`, which provides an elegant way to access route parameters. While you can use the `route()` method on form requests, with the new attribute you also get proper type hints 🚀

```php
<?php

use App\Models\Post;
use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Container\Attributes\RouteParameter;

class UpdatePost extends FormRequest
{
    public function authorize(#[RouteParameter('post')] Post $post): bool
    {
        return $this->user()->can('update', $post);
    }

    // ...
}

// Route definition
Route::put('/post/{post}', [PostsController::class, 'update']);
```

## Laravel Tip 💡: Disable Scope Bindings ([⬆️](#routing--requests-tips-cd-))

By default, Laravel assumes that nested route models are related, meaning it will automatically enforce parent-child relationships. However, if the models are unrelated, this can cause issues. Luckly, you can disable scope bindings by chaining the "withoutScopeBindings" method 🚀

```php
<?php

// The seller and category are now resolved separately
Route::get('stores/{seller}/{category:slug}', ShowStoreComponent::class)
    ->name('stores.show')
    ->withoutScopeBindings();
```

## Laravel Tip 💡: Detect User Language ([⬆️](#routing--requests-tips-cd-))

Laravel uses Symfony's HttpFoundation component, which comes with some nice goodies. If you are working with localization and need to detect the user's preferred language, you can just call "getPreferredLanguage" 🚀

```php
<?php

// Get the user's preferred language 🔥
$locale = request()->getPreferredLanguage(); // en_GB
```
