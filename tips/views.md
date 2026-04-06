# Views & Blade Tips ([cd ..](../README.md))

# Views & Blade Tips ([cd ..](../README.md))

- [Type Hinting for Blade](#laravel-tip--type-hinting-for-blade-️)
- [The "checked" Blade Directive](#laravel-tip--the-checked-blade-directive-️)
- [The "selected" Blade Directive](#laravel-tip--the-selected-blade-directive-️)
- [Access the Parent Loop Variable](#laravel-tip--access-the-parent-loop-variable-️)
- [Short Attribute Syntax](#laravel-tip--short-attribute-syntax-️)
- [Blade To HTML](#laravel-tip--blade-to-html-️)
- [The "aware" Blade Directive](#laravel-tip--the-aware-blade-directive-️)
- [The "readonly" Blade Directive](#laravel-tip--the-readonly-blade-directive-️)
- [The "includeWhen" Blade Directive](#laravel-tip--the-includewhen-blade-directive-️)
- [Render Inline Blade Templates](#laravel-tip--render-inline-blade-templates-️)
- [Useful Loop Properties](#laravel-tip--useful-loop-properties-️)
- [The "forelse" Blade Directive](#laravel-tip--the-forelse-blade-directive-️)
- [The "use" Blade Directive](#laravel-tip--the-use-blade-directive-️)
- [Better If Statements in Blade](#laravel-tip--better-if-statements-in-blade-️)
## Laravel Tip 💡: Type Hinting for Blade ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Type Hinting for Blade ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "checked" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "checked" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Access the Parent Loop Variable ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Access the Parent Loop Variable ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Short Attribute Syntax ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Short Attribute Syntax ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Blade To HTML ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Blade To HTML ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "aware" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "aware" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "readonly" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "readonly" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "includeWhen" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "includeWhen" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Render Inline Blade Templates ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Render Inline Blade Templates ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Useful Loop Properties ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Useful Loop Properties ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "forelse" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "forelse" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "use" Blade Directive ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: The "use" Blade Directive ([⬆️](#views--blade-tips-cd-))
![Laravel](https://img.shields.io/badge/Laravel-%3E%3D10.35-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-%3E%3D10.35-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
```php
// Instead of this 🥱
@php
use \App\Enums\TaskResult;
use \App\Enums\NotificationTypeEnum as NotificationType;
@endphp

// You can do this 🔥
@use('\App\Enums\TaskResult')
@use('\App\Enums\NotificationTypeEnum', 'NotificationType')
```
```php
// Instead of this 🥱
@php
use \App\Enums\TaskResult;
use \App\Enums\NotificationTypeEnum as NotificationType;
@endphp

// You can do this 🔥
@use('\App\Enums\TaskResult')
@use('\App\Enums\NotificationTypeEnum', 'NotificationType')
```
## Laravel Tip 💡: Better If Statements in Blade ([⬆️](#views--blade-tips-cd-))
## Laravel Tip 💡: Better If Statements in Blade ([⬆️](#views--blade-tips-cd-))
```html
@auth
    {{-- Equivalent to @if(auth()->check()) --}}
@endauth

@guest
    {{-- Equivalent to @if(auth()->guest()) --}}
@endguest

@isset($record)
    {{-- Equivalent to @if(isset($record)) --}}
@endisset

@empty($record)
    {{-- Equivalent to @if(empty($record)) --}}
@endempty

@production
    {{-- Equivalent to @if(app()->isProduction()) --}}
@endproduction

@env('local')
    {{-- Equivalent to @if(app()->environment('local')) --}}
@endenv
```
```html
@auth
    {{-- Equivalent to @if(auth()->check()) --}}
@endauth

@guest
    {{-- Equivalent to @if(auth()->guest()) --}}
@endguest

@isset($record)
    {{-- Equivalent to @if(isset($record)) --}}
@endisset

@empty($record)
    {{-- Equivalent to @if(empty($record)) --}}
@endempty

@production
    {{-- Equivalent to @if(app()->isProduction()) --}}
@endproduction

@env('local')
    {{-- Equivalent to @if(app()->environment('local')) --}}
@endenv
```

## Laravel Tip 💡: Type Hinting for Blade ([⬆️](#views--blade-tips-cd-))

We use Blade a lot, and if I have one thing to complain about, it's type hints. However, we can solve this issue by defining a @php block for all the variables used 🚀

```php
@php
    /* @var App\Models\Flight $flight */
@endphp

<div>
    // Your IDE will provide type hints for the property
    {{ $flight->name }}
</div>
```

## Laravel Tip 💡: The "checked" Blade Directive ([⬆️](#views--blade-tips-cd-))

Often, we need to conditionally mark an input as checked. While this can be done manually, Laravel provides a cool blade directive "checked" to do exactly that 🚀

```php
<input type="checkbox" name="active" value="active"
    {{ old('active', $user->active) ? 'checked' : '' }}
    @checked(old('active', $user->active)) />
```

## Laravel Tip 💡: The "selected" Blade Directive ([⬆️](#views--blade-tips-cd-))

When working with `<select>` elements, you often need to conditionally mark an `<option>` as selected.  
While you can do this manually with a ternary expression, Laravel provides the `@selected` Blade directive 🚀

```blade
{{-- Without @selected (cluttered) --}}
<option value="admin" {{ $user->role === 'admin' ? 'selected' : '' }}>
    Admin
</option>
```

```blade
{{-- With @selected (cleaner) --}}
<option value="admin" @selected($user->role === 'admin')>
    Admin
</option>
```

The `@selected` directive will automatically add the `selected` attribute when the given condition is `true`.  
This keeps your Blade templates cleaner and easier to read.

```blade
<select name="role">
    @foreach ($roles as $role)
        <option value="{{ $role->value }}" @selected($user->role === $role->value)>
            {{ $role->label }}
        </option>
    @endforeach
</select>
```

## Laravel Tip 💡: Access the Parent Loop Variable ([⬆️](#views--blade-tips-cd-))

Sometimes, when dealing with nested loops, you may want to keep track of the parent's iteration. Blade makes it incredibly easy, as you have access to the parent loop variable 🚀

```php
@foreach ($users as $user)
    @foreach ($user->posts as $post)
        @if ($loop->parent->first)
            // This is the first iteration of the parent loop.
        @endif
    @endforeach
@endforeach
```

## Laravel Tip 💡: Short Attribute Syntax ([⬆️](#views--blade-tips-cd-))

Did you know that Blade allows for short attribute syntax when passing to components? 🚀

```php
// Instead of this 😫
<x-profile :user-id="$userId"></x-profile>

// You can do this 😎
<x-profile :$userId></x-profile>
```

## Laravel Tip 💡: Blade To HTML ([⬆️](#views--blade-tips-cd-))

Did you know you can use Blade to render views as strings wherever you want? This is helpful as you can use Blade to build dynamic strings or even shell scripts, similar to how Envoy does 🚀

```php
<?php

// This renders the blade file welcome.blade.php into an HTML string
$rendered = view('welcome', ['foo' => 'bar'])->render();
```

## Laravel Tip 💡: The "aware" Blade Directive ([⬆️](#views--blade-tips-cd-))

Sometimes you might want to make parent props available to child components. While you could explicitly redefine the props for child component, Laravel ships with the "aware" directive to do exactly that 🚀

```html
<x-menu color="purple">
    <x-menu.item>...</x-menu.item>
    <x-menu.item>...</x-menu.item>
</x-menu>

<!-- /resources/views/components/menu/index.blade.php -->

@props(['color' => 'gray']) <!-- Color property is not accessible to child components -->
@aware(['color' => 'gray']) <!-- Color property is accessible to child components -->

<ul {{ $attributes->merge(['class' => 'bg-'.$color.'-200']) }}>
    {{ $slot }}
</ul>
```

## Laravel Tip 💡: The "readonly" Blade Directive ([⬆️](#views--blade-tips-cd-))

Often, we need to conditionally mark an input as readonly. While this can be done manually, Laravel provides a cool blade directive "readonly" to do exactly that 🚀

```html
<input
    type="email"
    name="email"
    {{ $user->isNotAdmin() ? 'readonly' : '' }}
    @readonly($user->isNotAdmin())
/>
```

## Laravel Tip 💡: The "includeWhen" Blade Directive ([⬆️](#views--blade-tips-cd-))

Have you ever needed to conditionally include a Blade view? While you could use "if" and "include" together, Laravel ships with the "includeWhen" and "includeUnless" directives to do exactly that 🚀

```php
// Instead of this 🥱
@if ($isAdmin)
    @include('components.impersonate')
@endif

// You can do this 🔥
@includeWhen($isAdmin, 'components.impersonate')

// even this
@includeUnless(! $isAdmin, 'components.impersonate')
```

## Laravel Tip 💡: Render Inline Blade Templates ([⬆️](#views--blade-tips-cd-))

Did you know you can render Blade templates inline? This is great for compiling Blade to HTML, like adding help texts in Nova or Filament or generating emails outside Laravel projects since it can work as a standalone package 🚀

```php
<?php

use Illuminate\Support\Facades\Blade;

return Blade::render('Hello, {{ $name }}', ['name' => 'Laravel']); // Hello, Laravel
```

## Laravel Tip 💡: Useful Loop Properties ([⬆️](#views--blade-tips-cd-))

When working with loops in Blade, you may need to check for odd iterations or calculate the remaining ones to adjust your UI. While you can do this manually, the "loop" variable has properties for almost everything you need 🚀

```php
@foreach ($users as $user)
    @if ($loop->first)
        This is the first iteration.
    @endif
 
    @if ($loop->last)
        This is the last iteration.
    @endif
 
    @if ($loop->even)
        This is an even iteration.
    @endif

    @if ($loop->odd)
        This is an odd iteration.
    @endif

    @if ($loop->remaining > 1)
        The remaining attribute holds the number of iterations left in the loop.
    @endif
@endforeach
```

## Laravel Tip 💡: The "forelse" Blade Directive ([⬆️](#views--blade-tips-cd-))

When looping over a collection, you have probably checked its count first to handle the empty state. But the "forelse" Blade directive has existed forever, and it does exactly that, elegantly 🚀

```php
<?php

// Instead of this 🥱
@if ($users->count())
    @foreach ($users as $user)
        <li>{{ $user->name }}</li>
    @endforeach
@else
    <p>No users</p>
@endif

// You can do this 🔥
@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse
```

## Laravel Tip 💡: The "use" Blade Directive ([⬆️](#views--blade-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D10.35-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

We have all probably used an enum in Blade at some point. While you can drop in raw PHP, Laravel v10 and upward have the "use" directive for exactly this 🚀

```php
// Instead of this 🥱
@php
use \App\Enums\TaskResult;
use \App\Enums\NotificationTypeEnum as NotificationType;
@endphp

// You can do this 🔥
@use('\App\Enums\TaskResult')
@use('\App\Enums\NotificationTypeEnum', 'NotificationType')
```

## Laravel Tip 💡: Better If Statements in Blade ([⬆️](#views--blade-tips-cd-))

If you are working with Blade, you will almost certainly use an if statement, and chances are, there is already a shortcut directive for what you need 🚀

```html
@auth
    {{-- Equivalent to @if(auth()->check()) --}}
@endauth

@guest
    {{-- Equivalent to @if(auth()->guest()) --}}
@endguest

@isset($record)
    {{-- Equivalent to @if(isset($record)) --}}
@endisset

@empty($record)
    {{-- Equivalent to @if(empty($record)) --}}
@endempty

@production
    {{-- Equivalent to @if(app()->isProduction()) --}}
@endproduction

@env('local')
    {{-- Equivalent to @if(app()->environment('local')) --}}
@endenv
```
