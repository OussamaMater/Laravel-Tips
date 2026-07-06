# Eloquent & Database Tips ([cd ..](../README.md))

- [Get Original Attributes](#laravel-tip--get-original-attributes-️)
- [Specify Custom Factories Path](#laravel-tip--specify-custom-factories-path-️)
- [Eager Loading with Specific Columns](#laravel-tip--eager-loading-with-specific-columns-️)
- [`is()` method in Laravel](#laravel-tip--ismethod-in-laravel-️)
- [A shorter "whereHas"](#laravel-tip--a-shorter-wherehas-️)
- [Dynamic Wheres](#laravel-tip--dynamic-wheres-️)
- [Quietly update your models](#laravel-tip--quietly-update-your-models-️)
- [Find Related IDs on a BelongsToMany Relationship](#laravel-tip--find-related-ids-on-a-belongstomany-relationship-️)
- [Get All Executed Queries](#laravel-tip--get-all-executed-queries-️)
- [The "Prunable" trait](#laravel-tip--the-prunable-trait-️)
- [The "whereBelongsTo" method](#laravel-tip--the-wherebelongsto-method-️)
- [The "whenQueryingForLongerThan" method](#laravel-tip--the-whenqueryingforlongerthan-method-️)
- [The "foreignIdFor" Method](#laravel-tip--the-foreignidfor-method-️)
- [Careful with "whereYear()"](#laravel-tip--careful-with-whereyear-️)
- [The "withCount" Method](#laravel-tip--the-withcount-method-️)
- [The "toQuery" method](#laravel-tip--the-toquery-method-️)
- [The "whenTableDoesntHaveColumn" and "whenTableHasColumn" methods](#laravel-tip--the-whentabledoesnthavecolumn-and-whentablehascolumn-methods-️)
- [The "withoutTimestamps" method](#laravel-tip--the-withouttimestamps-method-️)
- [Random Ordering](#laravel-tip--random-ordering-️)
- [Touching Relationships](#laravel-tip--touching-relationships-️)
- [Recursively Saving Models and Relationships](#laravel-tip--recursively-saving-models-and-relationships-️)
- [The "saveMany" method](#laravel-tip--the-savemany-method-️)
- [Query JSON Fields](#laravel-tip--query-json-fields-️)
- [The "toBase()" Method](#laravel-tip--the-tobase-method-️)
- [The "lazy()" Method](#laravel-tip--the-lazy-method-️)
- [The "value()" Method](#laravel-tip--the-value-method-️)
- [The "whereAll" and "whereAny" Methods](#laravel-tip--the-whereall-and-whereany-methods-️)
- [Limit Eager Loaded Relationships](#laravel-tip--limit-eager-loaded-relationships-️)
- [Define Casts as a Method](#laravel-tip--define-casts-as-a-method-️)
- [The "withExists" Method](#laravel-tip--the-withexists-method-️)
- [The "whereKey" Method](#laravel-tip--the-wherekey-method-️)
- [Avoid Columns Ambiguity](#laravel-tip--avoid-columns-ambiguity-️)
- [The "doesntHave" Method](#laravel-tip--the-doesnthave-method-️)
- [Mute All Model Events](#laravel-tip--mute-all-model-events-️)
- [Make use of "unguard"](#laravel-tip--make-use-of-unguard-️)
- [Customize the pivot Attribute Name](#laravel-tip--customize-the-pivot-attribute-name-️)
- [Increment and Decrement Methods](#laravel-tip--increment-and-decrement-methods-️)
- [Check if the Value of a Given Model Key Has Changed](#laravel-tip--check-if-the-value-of-a-given-model-key-has-changed-️)
- [The "getOrPut" Method](#laravel-tip--the-getorput-method-️)
- [Use the Higher Order "orWhere" Method](#laravel-tip--use-the-higher-order-orwhere-method-️)
- [Faster Queries with "whereIntegerInRaw"](#laravel-tip--faster-queries-with-whereintegerinraw-️)
- [The "upsert" Method](#laravel-tip--the-upsert-method-️)
- [No timestamp columns](#laravel-tip--no-timestamp-columns-️)
- [The "simplePaginate" Method](#laravel-tip--the-simplepaginate-method-️)
- [The "doesntExist" Method](#laravel-tip--the-doesntexist-method-️)
- [Clone Your Queries](#laravel-tip--clone-your-queries-️)
- [Hide Columns On The Fly](#laravel-tip--hide-columns-on-the-fly-️)
- [Disable Global Scopes](#laravel-tip--disable-global-scopes-️)
- [Hash Passwords Automatically](#laravel-tip--hash-passwords-automatically-️)
- [The "firstOr" Laravel](#laravel-tip--the-firstor-laravel-️)
- [Use "sole()" Instead of "firstOrFail()"](#laravel-tip--use-sole-instead-of-firstorfail-️)
- [The "latest" and "oldest" Methods](#laravel-tip--the-latest-and-oldest-methods-️)
- [Insert Or Ignore](#laravel-tip--insert-or-ignore-️)
- [Find Many](#laravel-tip--find-many-️)
- [Check If Your Model Has Changed Since Last Retrieval](#laravel-tip--check-if-your-model-has-changed-since-last-retrieval-️)
- [Customize the Default Timestamp Columns](#laravel-tip--customize-the-default-timestamp-columns-️)
- [Prevent Filling Unfillable Attributes](#laravel-tip--prevent-filling-unfillable-attributes-️)
- [Create New Records or Update Existing Ones](#laravel-tip--create-new-records-or-update-existing-ones-️)
- [Delete (Destroy) Records](#laravel-tip--delete-destroy-records-️)
- [Cast Values On The Fly](#laravel-tip--cast-values-on-the-fly-️)
- [The "valueOrFail" Method](#laravel-tip--the-valueorfail-method-️)
- [The "firstWhere" Method](#laravel-tip--the-firstwhere-method-️)
- [Prevent N+1 Issues](#laravel-tip--prevent-n1-issues-️)
- [Check if valid JSON](#laravel-tip--check-if-valid-json-️)
- [Count words occurances](#laravel-tip--count-words-occurances-️)
- [Shortcuts for Dropping Columns](#laravel-tip--shortcuts-for-dropping-columns-️)
- [Invisible Columns](#laravel-tip--invisible-columns-️)
- [Generated Columns](#laravel-tip--generated-columns-️)
- [Disable Model Events When Seeding](#laravel-tip--disable-model-events-when-seeding-️)
- [Use Default Models](#laravel-tip--use-default-models-️)
- [Permanently Delete Soft-Deleted Models](#laravel-tip--permanently-delete-soft-deleted-models-️)
- [Get Only Trashed Records](#laravel-tip--get-only-trashed-records-️)
- [Add Multiple Columns After Another](#laravel-tip--add-multiple-columns-after-another-️)
- [Cache Accessor Result](#laravel-tip--cache-accessor-result-️)
- [The "whereLike" method](#laravel-tip--the-wherelike-method-️)
- [Using Multiple IDs and Specific Columns with "find"](#laravel-tip--using-multiple-ids-and-specific-columns-with-find-️)
- [Load Relationship Count on the Fly](#laravel-tip--load-relationship-count-on-the-fly-️)
- [Move Column to First Position](#laravel-tip--move-column-to-first-position-️)
- [Latest of Many](#laravel-tip--latest-of-many-️)
- [A Cleaner Eager Loading Syntax](#laravel-tip--a-cleaner-eager-loading-syntax-️)
- [The "insertGetId" Method](#laravel-tip--the-insertgetid-method-️)
- [The "ddRawSql" Method](#laravel-tip--the-ddrawsql-method-️)
- [Avoid Duplicate Queries](#laravel-tip--avoid-duplicate-queries-️)
- [The New "CollectedBy" Attribute](#laravel-tip--the-new-collectedby-attribute-️)
- [Aggregate Functions](#laravel-tip--aggregate-functions-️)
- [The "toggle" method](#laravel-tip--the-toggle-method-️)
- [Get the Full Query Log](#laravel-tip--get-the-full-query-log-️)
- [The New "rawColumn" Method](#laravel-tip--the-new-rawcolumn-method-️)
- [Explain Eloquent Queries](#laravel-tip--explain-eloquent-queries-️)
- [The "firstOrNew" Method](#laravel-tip--the-firstornew-method-️)
- [The "withWhereHas" Method](#laravel-tip--the-withwherehas-method-️)
- [Update Pivot Columns](#laravel-tip--update-pivot-columns-️)
- [Prevent Accessing Missing Attributes](#laravel-tip--prevent-accessing-missing-attributes-️)
- [The New "incrementOrCreate" Method](#laravel-tip--the-new-incrementorcreate-method-️)
- [Keep an Eye on Open Connections](#laravel-tip--keep-an-eye-on-open-connections-️)
- [The "MassPrunable" trait](#laravel-tip--the-massprunable-trait-️)
- [Restore Trashed Models](#laravel-tip--restore-trashed-models-️)
- [Bootable Traits](#laravel-tip--bootable-traits-️)
- [Boot Traits with Attributes](#laravel-tip--boot-traits-with-attributes-️)
- [The New "whereAttachedTo" Method](#laravel-tip--the-new-whereattachedto-method-️)

## Laravel Tip 💡: Get Original Attributes ([⬆️](#eloquent--database-tips-cd-))

Laravel accessors allow you to transform your model attributes when retrieving them. But sometimes, you may wish to get the original value. Well, Laravel provides a method just for that: `getRawOriginal` 🚀

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Casts\Attribute;

class User extends Model
{
    protected function username(): Attribute
    {
        return Attribute::make(
            function (string $value, array $attributes) {
                return sprintf('%s#%s', $value, $attributes['app_id']);
            }
        );
    }
}

$user = User::create([
    'username' => 'oussama',
]);

$user->getOriginal('username'); // oussama#1234
$user->getRawOriginal('username'); // oussama
```

## Laravel Tip 💡: Specify Custom Factories Path ([⬆️](#eloquent--database-tips-cd-))

Laravel automatically resolves model factories if they exist in the Database\\Factories namespace. Sometimes you wish to move them. For example, if you're using Domain-Driven Design (DDD), you may want each domain to have its own factories. In such cases, you can instruct Laravel on how to resolve the factory by defining a newFactory method in your model. By doing so, you can perform additional logic too! For example return different factories for different environments.

```php
<?php

namespace App\Models;

use Database\Factories\UserFactory;
use Illuminate\Foundation\Auth\User as Authenticatable;

class User extends Authenticatable
{
    // ...

    protected static function newFactory()
    {
        // ... custom logic
        return new UserFactory();
    }
}
```

## Laravel Tip 💡: Eager Loading with Specific Columns ([⬆️](#eloquent--database-tips-cd-))

Did you know that when using eager loading with relationships, you may specify the exact columns you need? This will decrease memory usage 🚀

```php
<?php

$users = Post::with('author:id,name')->get();
```

## Laravel Tip 💡: `is()` method in Laravel ([⬆️](#eloquent--database-tips-cd-))

Did you know you can check whether or not two models are the same by using the `is()` helper? 🚀

```php
<?php

$user = User::find(1);  
$sameUser = User::find(1);  
$differentUser = User::find(2);

$user->is($sameUser); // true  
$user->is($differentUser); // false
```

## Laravel Tip 💡: A shorter "whereHas" ([⬆️](#eloquent--database-tips-cd-))

While Laravel's `whereHas` is excellent for retrieving records based on a specified relationship along with additional query constraints, there's a shortcut called "whereRelation" that accomplishes the same task 🚀

```php
<?php

// Before
User::whereHas('comments', function ($query) {
    $query->where('created_at', '>', now()->subDay());
})->get();

// After
User::whereRelation('comments', 'created_at', '>', now()->subDay())->get();
```

## Laravel Tip 💡: Dynamic Wheres ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel allows you to define dynamic "where" conditions? For example, you could do, `whereNameAndAge(name_value, age_value)` 🤯

Make sure to add the method name to your model's PHPDoc so your IDE does not complain, that's a bit too much magic for it to understand.

Curious about how it's done? Take a look at `Illuminate\Database\Query\Builder::dynamicWhere()`

```php
<?php

// select * from `users` where `name` = 'oussama' and `last_name` = 'mater'"
User::whereNameAndLastName('oussama', 'mater')->first();
```

## Laravel Tip 💡: Quietly update your models ([⬆️](#eloquent--database-tips-cd-))

When updating your Laravel models, you always trigger "Model Events," which are hooks enabling you to perform extra actions. You can disable this behavior by updating them quietly 🤫

```php
<?php

$user = Auth::user();

$user->name = 'Oussama Mater';

// Won't trigger Model Events
$user->saveQuietly();
$user->deleteQuietly();
$user->forceDeleteQuietly();
$user->restoreQuietly();
```

## Laravel Tip 💡: Find Related IDs on a BelongsToMany Relationship ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with the 'allRelatedId()' method to help you fetch all IDs for a belongsToMany relationship? Now you do 🚀

```php
<?php

class User extends Model
{
    public function roles()
    {
        return $this->belongsToMany(Role::class);
    }
}

$user = User::find(1);

$roleIds = $user->roles()->pluck('id')->toArray();
$roleIds = $user->roles()->allRelatedIds()->toArray();
```

## Laravel Tip 💡: Get All Executed Queries ([⬆️](#eloquent--database-tips-cd-))

Did you know you can listen to all executed queries in Laravel? This is not only useful for quick debugging; for instance, you can send a Slack notification if the query is slower than expected🚀

```php
<?php

DB::listen(function (QueryExecuted $query) {
    dump($query->sql); // select * from `users` where `users`.`id` = ? limit 1
    dump($query->bindings); // [0 => 1]
    dump($query->time); // 6.05
});
```

## Laravel Tip 💡: The "Prunable" trait ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel comes with a Prunable trait to permanently remove records, including the soft-deleted ones, based on a condition you define? 🚀

```php
<?php

// Define the pruning condition
class User extends Authenticatable
{
    use Prunable;

    public function prunable()
    {
        return static::query()
            ->whereNull('email_verified_at')
            ->where('created_at', '<', now()->subMonths(6));
    }
}

// Schedule the pruning command to run daily for example
$schedule->command(PruneCommand::class)->daily();
```

## Laravel Tip 💡: The "whereBelongsTo" method ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with a "whereBelongsTo" to get the parent model? This will make the code much more readable 🚀

```php
<?php

// This
$posts = Post::where('user_id', $user->id)->get();
// Or this is okay
$posts = Post::whereUserId($user->id)->get();

// But this is more readable
$posts = Post::whereBelongsTo($user)->get();
```

## Laravel Tip 💡: The "whenQueryingForLongerThan" method ([⬆️](#eloquent--database-tips-cd-))

Did you know that you can use "whenQueryingForLongerThan" to monitor slow queries? You can set the threshold in milliseconds. If a query exceeds the threshold, you can send notifications or grab a coffee with the mastermind behind the query 😂

```php
<?php

class AppServiceProvider extends ServiceProvider
{
    public function boot(): void
    {
        DB::whenQueryingForLongerThan(500, function (Connection $connection, QueryExecuted $event) {
            // Mastermind behind this query, let's grab a coffee ..
        });
    }
}
```

## Laravel Tip 💡: The "foreignIdFor" Method ([⬆️](#eloquent--database-tips-cd-))

When defining foreign IDs, Laravel offers multiple methods, one of which is "foreignIdFor()". This method snake cases the model name and appends "id" to it. Not only does it make your code more readable, but you can quickly navigate to the model from the migration 🚀

```php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

Schema::table('posts', function (Blueprint $table) {
    $table->id();
    $table->string('title');
    $table->foreignIdFor(User::class); // user_id
    $table->timestamps();
});
```

## Laravel Tip 💡: Careful with "whereYear()" ([⬆️](#eloquent--database-tips-cd-))

Be careful when using `whereYear`; even if your column is indexed, it won't be used, and the database will perform a full table scan. Instead, opt for using ranges 🚀

```php
<?php

DB::table('user_posts')
    ->select('user_id', DB::raw('COUNT(*) as count'))
    ->whereYear('created_at', 2023)
    ->groupBy('user_id')
    ->get();
// select `user_id`, COUNT(*) as count from `user_posts` where year(`created_at`) = ? group by `user_id`

DB::table('user_posts')
    ->select('user_id', DB::raw('COUNT(*) as count'))
    ->whereBetween('created_at', ['2023-01-01 00:00:00', '2024-01-01 00:00:00'])
    ->groupBy('user_id')
    ->get();
// select `user_id`, COUNT(*) as count from `user_posts` where `created_at` between ? and ? group by `user_id`
```

## Laravel Tip 💡: The "withCount" Method ([⬆️](#eloquent--database-tips-cd-))

Did you know that you can use "withCount" to get the count of a related relationship without loading it? This is really useful, for example, when displaying statistics 🚀

```php
<?php

$users = User::withCount(['posts'])->get();

// $users->posts_count
```

## Laravel Tip 💡: The "toQuery" method ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with a method called "toQuery"? This method allows you to update a collection using a single query statement by running a "whereIn" 🚀

```php
<?php

$users = User::where('status', 'VIP')->get();

// Instead of this
foreach ($users as $user) {
    $user->update(['status' => 'Administrator']);
}

// Do this instead
$users->toQuery()->update(['status' => 'Administrator']);
```

## Laravel Tip 💡: The "whenTableDoesntHaveColumn" and "whenTableHasColumn" methods ([⬆️](#eloquent--database-tips-cd-))

Laravel 9 and onward ship with 2 schema methods, 'whenTableDoesntHaveColumn' and 'whenTableHasColumn', which allow you to drop or create a column if it exists or not. This is really helpful when you have multiple environments where schemas can get out of sync quickly.

```php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

// Will create the email column only if it does not exist
Schema::whenTableDoesntHaveColumn('users', 'email', function(Blueprint $table){
    $table->string('email')->unique();
});

// Will drop the email column only if it exists
Schema::whenTableHasColumn('users', 'email', function(Blueprint $table){
    $table->dropColumn('email');
});
```

## Laravel Tip 💡: The "withoutTimestamps" method ([⬆️](#eloquent--database-tips-cd-))

Did you know that if you want to update a model without modifying its `updated_at` timestamp, you can use the 'withoutTimestamps' method? 🚀

```php
<?php

// The updated_at column will not be updated
Post::withoutTimestamps(fn () => $post->increment(['reads']));
```

## Laravel Tip 💡: Random Ordering ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel comes with the "inRandomOrder" method, which sorts query results randomly? 🚀

```php
$randomUser = DB::table('users')
->inRandomOrder()
->first();
```

## Laravel Tip 💡: Touching Relationships ([⬆️](#eloquent--database-tips-cd-))

Laravel automatically updates "updated_at" in many-to-many relationships, and it also ships with "setTouchedRelations" method to manually update related models in one-to-one and one-to-many relationships 🚀

```php
<?php

$user = User::firstOrFail();
$user->setTouchedRelations(['posts']);

// The 'updated_at' of all related posts will be updated
$user->save();
```

## Laravel Tip 💡: Recursively Saving Models and Relationships ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with the "push" method, allowing you to save models and all related relationships recursively, without having to go over them one by one? 🚀

```php
<?php

$post = Post::find(1);

$post->comments[0]->message = 'Message';
$post->comments[0]->author->name = 'Author Name';

// Instead of these
$post->comments[0]->author->save();
$post->comments[0]->save();

// You can do this
$post->push();
```

## Laravel Tip 💡: The "saveMany" method ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel allows you to save multiple related models at once by using the 'saveMany' method? 🚀

```php
<?php

$post = Post::find(1);

$post->comments()->saveMany([
    new Comment(['message' => 'A new comment.']),
    new Comment(['message' => 'Another new comment.']),
]);
```

## Laravel Tip 💡: Query JSON Fields ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel allows you to query JSON fields in databases that support JSON column types? 🚀

```php
<?php

// Will return all users where the preferences.dining.meal field is equal to 'salad'
DB::table('users')
    ->where('preferences→dining→meal', 'salad')
    ->get();

// Will return all users where the languages array contains 'en' and 'de'
DB::table('users')
    ->whereJsonContains('options→languages', ['en', 'de'])
    ->get();

// Will return all users where the languages array has more than one element
DB::table('users')
    ->whereJsonLength('options→languages', '>', 1)
    ->get();
```

## Laravel Tip 💡: The "toBase()" Method ([⬆️](#eloquent--database-tips-cd-))

Sometimes, you may need to load a large amount of data, but you don't need the hydrated models. In these scenarios, you can use the "toBase()" method provided by Laravel to save on memory usage 🚀

```php
<?php

// This collection will consist of PHP objects
// and will not include hydrated models
$users = User::toBase()->get();
```

## Laravel Tip 💡: The "lazy()" Method ([⬆️](#eloquent--database-tips-cd-))

Need to process a large dataset without blowing up your memory? Use `lazy()` to stream records one by one via a LazyCollection instead of loading everything into memory at once 🚀

```php
<?php

// ❌ Loads all users into memory first
User::where('active', true)
    ->get()
    ->each(function (User $user): void {
        SendReminder::dispatch($user);
    });

// ✅ Streams records instead of loading everything at once
User::where('active', true)
    ->lazy()
    ->each(function (User $user): void {
        SendReminder::dispatch($user);
    });
```

## Laravel Tip 💡: The "value()" Method ([⬆️](#eloquent--database-tips-cd-))
  
Sometimes, you only need a single value instead of the entire row. Laravel comes with the "value()" method, which return the value of the column directly 🚀

```php
<?php

$email = DB::table('users')->where('name', 'John')->value('email');

dd($email); // john@example.com
```

## Laravel Tip 💡: The "whereAll" and "whereAny" Methods ([⬆️](#eloquent--database-tips-cd-))

Laravel v10.47.0 has just been released, featuring four new methods: "whereAll," "whereAny," "orWhereAll," and "orWhereAny." These methods allow you to compare a value against multiple columns 🚀

```php
<?php

$search = 'ous%';

// Instead of this
User::query()
    ->where(function($query) use ($search) {
        $query
            ->where('first_name', 'LIKE', $search)
            ->where('last_name', 'LIKE', $search);
    })
    ->get();

// You can now do this
User::query()
    ->whereAll(['first_name', 'last_name'], 'LIKE', $search)
    ->get();

User::query()
    ->whereAny(['first_name', 'last_name'], 'LIKE', $search)
    ->get();

// Which results in the following queries

// select * from `users` where (`first_name` LIKE 'ous%' and `last_name` LIKE 'ous%')
// select * from `users` where (`first_name` LIKE 'ous%' or `last_name` LIKE 'ous%')

// You can also use "orWhereAll" and "orWhereAny".
```

## Laravel Tip 💡: Limit Eager Loaded Relationships ([⬆️](#eloquent--database-tips-cd-))

In Laravel versions 10 and below, we couldn't limit eager loaded relationships natively. Well, guess what? In Laravel 11, we can! 🚀

```php
<?php

User::with([
    'posts' => fn ($query) => $query->limit(5)
])->paginate();
```

## Laravel Tip 💡: Define Casts as a Method ([⬆️](#eloquent--database-tips-cd-))

In Laravel versions 10 and below, we had to define casts as properties which made it a bit messy to pass arguments. In Laravel 11, we can define casts as a method! 🚀

```php
<?php

namespace App\Models;

use App\Casts\Json;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
   // Laravel ≤ 10 😔
   protected $casts = [
       'statuses' => AsEnumCollection::class.':'.ServerStatus::class,
   ];

   // Laravel 11 😎
   protected function casts(): array
   {
       return [
           'statuses' => AsEnumCollection::of(ServerStatus::class),
       ];
   }
}
```

## Laravel Tip 💡: The "withExists" Method ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with a method called `withExists` which allows you to check if a model has a relationship or not? This is really helpful for conditional logics 🚀

```php
<?php

$user = User::query()
    ->withExists('posts as is_author')
    ->get();

/*
    select
        `users`.*,
        exists (select * from `posts` where `users`.`id` = `posts`.`user_id`) as `is_author`
    from `users`
*/

$user->is_author; // Will be either true or false.
```

## Laravel Tip 💡: The "whereKey" Method ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with the "whereKey" method? It makes your "where in" statements more readable, and well, you don't have to remember the name of the primary key 🚀

```php
<?php

// 😕 Instead of doing this
Post::whereIn('id', [1,2,3])->get();
Post::whereNotIn('id', [1,2,3])->get();

// 😎 You can do this
Post::whereKey([1,2,3])->get();
Post::whereKeyNot([1,2,3])->get();
```

## Laravel Tip 💡: Avoid Columns Ambiguity ([⬆️](#eloquent--database-tips-cd-))

I'm sure we've all encountered column name ambiguity when building queries at least once. To avoid that, you can use the "qualifyColumn" method, which prefixes the column with the table name 🚀

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;

class Team extends Model
{
    use HasFactory;

    protected $fillable = [
        'name',
    ];

    public function servers(): HasMany
    {
        // Use qualifyColumn() to avoid collision
        // with the 'name' column on the Team model
        return $this->hasMany(Server::class)->orderBy(
            (new Server)->qualifyColumn('name')
        );
    }
}
```

## Laravel Tip 💡: The "doesntHave" Method ([⬆️](#eloquent--database-tips-cd-))

Sometimes, you may want to retrieve all the models that do not have a relationship. While you can achieve this using a query builder, Laravel already ships with the "doesntHave" method, which reads so well 🚀

```php
<?php

use App\Models\Post;

// Posts that do not have the "comments" relationship
$posts = Post::doesntHave('comments')->get();

/*
select *
from `posts`
where
    not exists (
        select *
        from comments
        where
            `posts`.`id` = `comments`.`post_id`
    )
*/
```

## Laravel Tip 💡: Mute All Model Events ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may want to mute all events fired by a model. Laravel ships with the "withoutEvents" method that accomplishes exactly that 🚀

```php
<?php

use App\Models\User;

// This will mute all model events 🤔
$user = User::withoutEvents(function () {
    User::findOrFail(1)->delete();
    
    return User::find(2);
});
```

## Laravel Tip 💡: Make use of "unguard" ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel allows you to unguard a model? While you can still use the forceFill method, this approach enables you to unguard multiple models at once, which is really useful for seeding the database 🚀

```php
<?php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Flight extends Model
{
    protected $fillable = ['name'];
}

Model::unguard();

// You can have *multiple* models unguarded
Flight::create([
    'name' => 'flight',
    'not_in_fillable' => true,
]);

Model::reguard();
```

## Laravel Tip 💡: Customize the pivot Attribute Name ([⬆️](#eloquent--database-tips-cd-))

We all use many-to-many relationships. In those cases, the intermediate table is accessed via the pivot attribute. Renaming it to something more expressive can make the code more readable 🚀

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;

class User extends Model
{
    public function podcasts(): BelongsToMany
    {
        return $this->belongsToMany(Podcast::class)
            ->as('subscription')
            ->withTimestamps();
    }
}

$users = User::with('podcasts')->get();

foreach ($users->flatMap->podcasts as $podcast) {
    // Instead of $podcast->pivot->created_at
    echo $podcast->subscription->created_at;
}
```

## Laravel Tip 💡: Increment and Decrement Methods ([⬆️](#eloquent--database-tips-cd-))

Sometimes we need to update a value by incrementing or decrementing it. Usually, we would write a query to achieve this, but Laravel comes with elegant methods to do so 🚀

```php
<?php

// Increment votes by 1
DB::table('users')->increment('votes');

// Increment votes by 5
DB::table('users')->increment('votes', 5);

// Decrement votes by 1
DB::table('users')->decrement('votes');

// Decrement votes by 5
DB::table('users')->decrement('votes', 5);

// Increment votes by 1 and set the name to John
DB::table('users')->increment('votes', 1, ['name' => 'John']);

// You can increment multiple columns at once
DB::table('users')->incrementEach([
    'votes' => 5,    // Will increment votes by 5
    'balance' => 100, // Will increment balance by 100
]);

// You can also use them with Eloquent
User::query()->incrementEach([
    'votes' => 5,    // Will increment votes by 5
    'balance' => 100  // Will increment balance by 100
]);
```

## Laravel Tip 💡: Check if the Value of a Given Model Key Has Changed ([⬆️](#eloquent--database-tips-cd-))

Sometimes, we wish to check if the value of a given model key has been affected by a change or not. Laravel ships with the "originalIsEquivalent()" method to do exactly that 🚀

```php
<?php

$user = User::firstOrFail(); // ['name' => 'old']

$user->name = 'old'; // Keep the old value

$user->originalIsEquivalent('name'); // true

$user->name = 'new'; // Change the value

$user->originalIsEquivalent('name'); // false
```

## Laravel Tip 💡: The "getOrPut" Method ([⬆️](#eloquent--database-tips-cd-))

When using collections, sometimes we want to retrieve the value of an existing key but insert it if it does not exist. While this can be achieved using the "get" and "put" methods, Laravel offers a handy method called "getOrPut" that does the same 🚀

```php
$collection = collect(['price' => 100]);

// Check and set value if not exists
if (!$collection->has('name')) {
    $collection->put('name', 'Desk');
}
$value = $collection->get('name');

// Or use getOrPut() for the same operation
$value = $collection->getOrPut('name', 'Desk');
```

## Laravel Tip 💡: Use the Higher Order "orWhere" Method ([⬆️](#eloquent--database-tips-cd-))

Laravel supports "Higher Order Messages" with collections, which are cool shortcuts that we use. But did you know that you can make use of them when writing eloquent queries? 🚀

```php
// tip-100.php
<?php

// Instead of this 😫
User::popular()->orWhere(function (Builder $query) {
    $query->active();
})->get()

// You can do this 😎
User::popular()->orWhere->active()->get();
```

## Laravel Tip 💡: Faster Queries with "whereIntegerInRaw" ([⬆️](#eloquent--database-tips-cd-))

When using a whereIn query with non-user input, opt for whereIntegerInRaw. This speeds up your query by skipping PDO bindings and Laravel's security measures against SQL injection 🚀

```php
<?php

// Instead of using whereIn()
Product::whereIn('id', range(1, 10000))->get();

// Use WhereIntegerInRaw()
Product::whereIntegerInRaw('id', range(1, 10000))->get();
```

## Laravel Tip 💡: The "upsert" Method ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may wish to update a bunch of records or create them if they do not exist. Laravel ships with a cool method "upsert" to do exactly that 🚀

```php
<?php

/*
This will update the price of all the records that match
the given departure and destination or create them
*/
Flight::upsert([
    ['departure' => 'Oakland', 'destination' => 'San Diego', 'price' => 99],
    ['departure' => 'Chicago', 'destination' => 'New York', 'price' => 150]
], uniqueBy: ['departure', 'destination'], update: ['price']);
```

## Laravel Tip 💡: No timestamp columns ([⬆️](#eloquent--database-tips-cd-))

Sometimes, your table might not have the "created_at" and "updated_at" columns. You can instruct Laravel not to update them by setting "timestamps" to false 🚀

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Flight extends Model
{
    /**
     * Indicates if the model should be timestamped.
     *
     * @var bool
     */
    public $timestamps = false;
}
```

## Laravel Tip 💡: The "simplePaginate" Method ([⬆️](#eloquent--database-tips-cd-))

Sometimes, when paginating your models, you may only need a "next" and "previous" buttons. For this, you can use the "simplePaginate" method instead of the regular paginate 🚀

```php
<?php

$users = User::paginate(15);

/*
Will result in the following keys
[
    "current_page",
    "data",
    "first_page_url",
    "from",
    "last_page",
    "last_page_url",
    "links",
    "next_page_url",
    "path",
    "per_page",
    "prev_page_url",
    "to",
    "total",
];
*/
$users = User::simplePaginate(15);

/*
Will result in the following keys
[
    "current_page",
    "data",
    "first_page_url",
    "from",
    "next_page_url",
    "path",
    "per_page",
    "prev_page_url",
    "to",
];
*/
```

## Laravel Tip 💡: The "doesntExist" Method ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may want to check if certain records do not exist in the database. While checking the count or using the exists() method can do the trick, Laravel ships with the "doesntExist" method to do it elegantly 🚀

```php
// Image 5: tip-116.php
<?php

// This is okay 😊
if (User::count() === 0) {
}

// This is good 😊
if (! User::exists()) {
}

// This is better 😎
if (User::doesntExist()) {
}
```

## Laravel Tip 💡: Clone Your Queries ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may need to reuse the same base query for multiple filtering. Laravel ships with a "clone" method to do exactly that 🚀

```php
<?php

// Base query, common conditions
$query = User::query()->where('created_at', '<', now()->subMonths(3));

$verified_users = $query->clone()->whereNotNull('email_verified_at')->get();

// This can be customized further if needed
$unverified_users = $query->clone()->whereNull('email_verified_at')->get();
```

## Laravel Tip 💡: Hide Columns On The Fly ([⬆️](#eloquent--database-tips-cd-))

Sometimes, you may want to hide model attributes that were not defined in the "hidden" array. Laravel allows you to do this on the fly using the "makeHidden" method 🚀

```php
<?php

$users = User::all()->makeHidden(['address', 'phone_number']);
```

## Laravel Tip 💡: Disable Global Scopes ([⬆️](#eloquent--database-tips-cd-))

Laravel allows you to apply global scopes to your models, but sometimes you may wish to disable them for a specific query. You can do this by chaining the "withoutGlobalScope" method 🚀

```php
<?php

// Remove all of the global scopes
User::withoutGlobalScopes()->get();

// Remove a single global scope
User::withoutGlobalScope(FirstScope::class)->get();

// Remove some of the global scopes
User::withoutGlobalScopes([
    FirstScope::class, SecondScope::class
])->get();
```

## Laravel Tip 💡: Hash Passwords Automatically ([⬆️](#eloquent--database-tips-cd-))

When creating users, we often use the Hash facade, but did you know that Laravel comes with a "hashed" cast that will automatically hash your user's password? 🚀

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    protected function casts(): array
    {
        return [
            'password' => 'hashed',
        ];
    }
}

$user = User::create([
    // ...
    'password' => 'password', // Instead of Hash::make('password')
]);
```

## Laravel Tip 💡: The "firstOr" Laravel ([⬆️](#eloquent--database-tips-cd-))

Sometimes, you may want to execute some actions when no record is found, beyond just creating a new instance. The "firstOr" method allows you to do exactly that 🚀

```php
<?php

$user = User::where('email', $request->input('email'))->firstOr(function () {
    // Execute some logic

    // Create and return a new user
    return User::create([
        // ...
    ]);
});
```

## Laravel Tip 💡: Use "sole()" Instead of "firstOrFail()" ([⬆️](#eloquent--database-tips-cd-))

When querying a record that should be unique (e.g., by email), "firstOrFail()" silently returns the first record even if duplicates exist. Use "sole()" instead to ensure exactly one record matches the query 🚀

```php
<?php

// ❌ Assumes only one record exists
$user = User::where('email', $email)->firstOrFail();

// ✅ Ensures exactly one record exists
$user = User::where('email', $email)->sole();
```

## Laravel Tip 💡: The "latest" and "oldest" Methods ([⬆️](#eloquent--database-tips-cd-))

We often order models in ascending or descending order using the "orderBy" method. But did you know that Laravel comes with two methods, "latest" and "oldest," that do exactly that? 🚀

```php
<?php

// Instead of this 🥱
User::orderBy('created_at', 'desc')->get();
User::orderBy('created_at', 'asc')->get();

// Do this 😎
User::latest()->get();
User::oldest()->get();

// You can specify keys other than created_at
User::latest('id')->get();
User::oldest('id')->get();
```

## Laravel Tip 💡: Insert Or Ignore ([⬆️](#eloquent--database-tips-cd-))

Sometimes, you might want to ignore errors when inserting data. Laravel comes with the "insertOrIgnore" method that does exactly that 🚀

```php
<?php

DB::table('users')->insertOrIgnore([
    ['id' => 1, 'email' => 'sisko@example.com'],
    ['id' => 2, 'email' => 'archer@example.com'],
]);

// insert ignore into `users` (`email`, `id`) values (?, ?), (?, ?)
```

## Laravel Tip 💡: Find Many ([⬆️](#eloquent--database-tips-cd-))

Did you know that you can pass multiple IDs to the `find()` method? Laravel also ships with a slightly more readable method, `findMany()`, which does the same thing! 🚀

```php
<?php

// Instead of this
$users = User::query()->whereIn('id', [1, 2, 3])->get();

// Do this
$users = User::find([1, 2, 3]);

// Even better, find() calls findMany() internally, so skip it and be expli
$users = User::findMany([1, 2, 3]);
```

## Laravel Tip 💡: Check If Your Model Has Changed Since Last Retrieval ([⬆️](#eloquent--database-tips-cd-))

Did you know Laravel ships with the `isDirty()` method, which allows you to check if one or more attributes have changed since the last time you retrieved the model? 🚀

```php
<?php

use App\Models\User;

$user = User::create([
    'first_name' => 'John',
    'last_name' => 'Doe',
    'age' => 20,
]);

$user->age = 21;

$user->isDirty(); // true
$user->isDirty('age'); // true
$user->isDirty('first_name'); // false
$user->isDirty(['first_name', 'age']); // true
$user->isDirty(['first_name', 'last_name']); // false

$user->save();

$user->isDirty(); // false
```

## Laravel Tip 💡: Customize the Default Timestamp Columns ([⬆️](#eloquent--database-tips-cd-))

Sometimes, you might need to customize the default timestamp columns, or you might already have an old table for which you are creating a model. Luckily, it is super simple to do so 🚀

```php
<?php

class Flight extends Model
{
    const CREATED_AT = 'creation_date';
    const UPDATED_AT = 'updated_date';
}
```

## Laravel Tip 💡: Prevent Filling Unfillable Attributes ([⬆️](#eloquent--database-tips-cd-))

Did you know you can configure Laravel to throw an exception when attempting to fill an unfillable attribute? This is helpful during development to catch missed or forgotten attributes before getting to prod 🚀

```php
<?php

use Illuminate\Database\Eloquent\Model;

Model::preventSilentlyDiscardingAttributes(! $this->app->isProduction());
```

## Laravel Tip 💡: Create New Records or Update Existing Ones ([⬆️](#eloquent--database-tips-cd-))

We've all been in a situation where we want to check if a record exists so we can update it, or create it if it does not. Laravel ships with the `updateOrCreate` method to do exactly that 🚀

```php
<?php

$flight = Flight::updateOrCreate(
    // If we can't find a flight with the following criteria,
    ['departure' => 'Oakland', 'destination' => 'San Diego'],
    // we will create it with the following data
    ['price' => 99, 'discounted' => 1]
);
```

## Laravel Tip 💡: Delete (Destroy) Records ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel ships with the `destroy` method, which allows you to delete records by their primary key? 🚀

```php
<?php

// Instead of this 😢
Flight::find(1)->delete()

// Do this 😎
Flight::destroy(1);

Flight::destroy(1, 2, 3); // works with variadic arguments

Flight::destroy([1, 2, 3]); // arrays

Flight::destroy(collect([1, 2, 3])); // and also collections!
```

## Laravel Tip 💡: Cast Values On The Fly ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may need to apply casts while executing a query. Luckily, you can do that on the fly with the "withCasts" method that Laravel ships with 🚀

```php
<?php

$users = User::select([
    'users.*',
    'last_posted_at' => Post::selectRaw('MAX(created_at)')
        ->whereColumn('user_id', 'users.id')
])->withCasts([
    // Casting the raw string 'last_posted_at' to a datetime
    'last_posted_at' => 'datetime'
])->get();
```

## Laravel Tip 💡: The "valueOrFail" Method ([⬆️](#eloquent--database-tips-cd-))

We often use the "firstOrFail" method to get a single value from the resulting model. Did you know that Laravel ships with the "valueOrFail" method, which allows you to do exactly that? 🚀

```php
<?php

// Instead of this
$flight = Flight::where('legs', '>', 3)->firstOrFail();
$flightName = $flight->name;

// Do this
$flightName = Flight::where('legs', '>', 3)->valueOrFail('name');
```

## Laravel Tip 💡: The "firstWhere" Method ([⬆️](#eloquent--database-tips-cd-))

We often need to get the first record matching a where statement. While "where()" combined with "first()" does the job, Laravel ships with a shortcut "firstWhere()" to do exactly that 🚀

```php
<?php

// Instead of this 😞
$user = User::query()->where('name', 'john')->first();

// Do this 😎
$user = User::query()->firstWhere('name', 'john');
```

## Laravel Tip 💡: Prevent N+1 Issues ([⬆️](#eloquent--database-tips-cd-))

Eager loading can significantly improve performance. Use the "preventLazyLoading" method to ensure all relationships are eager-loaded during development and customize its behavior for violations 🚀

```php
<?php

use Illuminate\Database\Eloquent\Model;

// In your AppServiceProvider
public function boot(): void
{
    // This ensures lazy loading is prevented in your dev environment
    Model::preventLazyLoading(! $this->app->isProduction());

    // You can customize the behavior for lazy loading violations
    Model::handleLazyLoadingViolationUsing(function (Model $model, string $relation) {
        $class = $model::class;

        info("Attempted to lazy load [{$relation}] on model [{$class}].");
    });
}
```

## Laravel Tip 💡: Check if valid JSON ([⬆️](#eloquent--database-tips-cd-))

We often need to check if a given string is valid JSON. Laravel provides an elegant method, "isJson", to help you with this. It uses the new "json_validate" function in PHP 8.3, and "json_decode" for earlier versions 🚀

```php
<?php

use Illuminate\Support\Str;

// The cool thing is, on the day you upgrade to PHP 8.3, if you haven't already,
// you will automatically be using the new "json_validate()" function
// instead of "json_decode()"

Str::isJson('[1,2,3]'); // true

Str::isJson('{"first": "John", "last": "Doe"}'); // true

Str::isJson('{first: "John", last: "Doe"}'); // false
```

## Laravel Tip 💡: Count words occurances ([⬆️](#eloquent--database-tips-cd-))

Ever needed to count the occurrences of a word in a sentence? Laravel ships with the "substrCount" method to do exactly that 🚀

```php
<?php

use Illuminate\Support\Str;

Str::substrCount('My name is Bond, James Bond', 'Bond'); // 2
```

## Laravel Tip 💡: Shortcuts for Dropping Columns ([⬆️](#eloquent--database-tips-cd-))

Need to drop some framework-specific columns? You don’t have to specify them manually, Laravel provides shortcuts to do exactly that 🚀

```php
<?php

Schema::table('users', function (Blueprint $table) {
    $table->dropColumn(['created_at', 'updated_at']);
    $table->dropTimestamps();

    $table->dropColumn(['deleted_at']);
    $table->dropSoftDeletes();

    $table->dropColumn(['remember_token']);
    $table->dropRememberToken();

    $table->dropColumn(['morphable_id', 'morphable_type']);
    $table->dropMorphs('morphable');
});
```

## Laravel Tip 💡: Invisible Columns ([⬆️](#eloquent--database-tips-cd-))

If you are using MySQL/MariaDB as your database, you can leverage invisible columns. These columns remain hidden in 'SELECT * ' statements, which is perfect for handling sensitive information and precomputed data 🚀

```php
<?php

use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

// Note that this works for MariaDB/MySQL
Schema::table('users', function (Blueprint $table) {
    // Useful for storing secrets
    $table->string('secret')->nullable()->invisible();

    // Or for precomputed columns
    $table->string('posts_count')->default(0)->invisible();
});

// The attribute is not even present on the Eloquent object
$user = User::first();
$user->secret; // null

// You have to explicitly select the column
$user = User::select('secret')->first();
$user->secret; // SUEGQs8klF30CLSi
```

## Laravel Tip 💡: Generated Columns ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel can handle generated columns in migrations out of the box? No need to write raw SQL in your migration to create these columns 🚀

```php
<?php

return new class extends Migration
{
    public function up(): void
    {
        Schema::create('products', function (Blueprint $table) {
            // ...

            $table->decimal('unit_price');
            $table->integer('quantity');

            // Works on MariaDB / MySQL / PostgreSQL / SQLite
            $table->decimal('full_price')->storedAs('unit_price * quantity');

            // ...
        });
    }
};
```

## Laravel Tip 💡: Disable Model Events When Seeding ([⬆️](#eloquent--database-tips-cd-))

In most cases, when seeding the database, you don't need to fire model events. You can use the "WithoutModelEvents" trait to mute those events, making your seeders slightly faster 🚀

```php
<?php

namespace Database\Seeders;

use Illuminate\Database\Seeder;
use Illuminate\Database\Console\Seeds\WithoutModelEvents;

class DatabaseSeeder extends Seeder
{
    use WithoutModelEvents; // Will mute all model events

    public function run(): void
    {
        $this->call([
            UserSeeder::class,
            PostSeeder::class,
            CommentSeeder::class,
        ]);
    }
}
```

## Laravel Tip 💡: Use Default Models ([⬆️](#eloquent--database-tips-cd-))

When working with "hasOne" or "belongsTo" relationships, we often check whether they are nullable before accessing their properties. In such cases, you can use default models to ensure you never get null values 🚀

```php
<?php

public function user(): BelongsTo
{
    return $this->belongsTo(User::class)->withDefault([
        'name' => 'Guest Author',
    ]);
}

// Now, instead of checking this every time
Post::first()->user->name ?? 'Guest Author'; // 'Guest Author'

// You can be confident that when a user is null, the default will be used
Post::first()->user->name; // 'Guest Author'
```

## Laravel Tip 💡: Permanently Delete Soft-Deleted Models ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may want to permanently remove soft-deleted models. You can use "forceDelete()" for that, or the new "forceDestroy()" method introduced in Laravel v11.21 🚀

```php
<?php

// Laravel < v11.20
$flight = Flight::find(1);
$flight->forceDelete();

// Laravel v11.21
Flight::forceDestroy(1); // You can also pass an array of IDs
```

## Laravel Tip 💡: Get Only Trashed Records ([⬆️](#eloquent--database-tips-cd-))

When working with soft-deleted models, you may need to get only the trashed records. While you can manually filter the query using the "deleted_at" column, there's an "onlyTrashed()" method to do exactly that 🚀

```php
<?php

// Instead of manually specifying 'deleted_at'
$trashedUsers = User::query()->whereNotNull('deleted_at')->get();

// You can use onlyTrashed(), which is both easier and more readable
$trashedUsers = User::query()->onlyTrashed()->get();
```

## Laravel Tip 💡: Add Multiple Columns After Another ([⬆️](#eloquent--database-tips-cd-))

Did you know that you can add multiple columns after a specific column using the "after" method?  🚀

```php
<?php

Schema::table('users', function (Blueprint $table) {
    $table->after('password', function (Blueprint $table) {
        $table->string('address_line1');
        $table->string('address_line2');
        $table->string('city');
    });
});
```

## Laravel Tip 💡: Cache Accessor Result ([⬆️](#eloquent--database-tips-cd-))

When working with accessors, objects are cached by default. However, if you have a computationally intensive accessor for a primitive value, like a string, you can enable caching for it using the "shouldCache()" method 🚀

```php
<?php

protected function hash(): Attribute
{
    return Attribute::make(
        get: fn (string $value) => bcrypt(gzuncompress($value)),
    )->shouldCache();
}
```

## Laravel Tip 💡: The "whereLike" method ([⬆️](#eloquent--database-tips-cd-))

We often use "where like" statements in our apps. Did you know Laravel ships with a "whereLike" method, which takes it a step further by allowing the like statement to be case insensitive? 🚀

```php
<?php
// Instead of this
User::query()->where('name', 'like', 'Jo%')->get();

// You can do this
User::query()->whereLike('name', 'Jo%')->get();

// You can even specify whether it should be case sensitive
User::query()->whereLike('name', 'Jo%', caseSensitive: true)->get();
// Query: select * from `users` where `name` like binary 'Jo%'
```

## Laravel Tip 💡: Using Multiple IDs and Specific Columns with "find" ([⬆️](#eloquent--database-tips-cd-))

We often use "find()", but did you know you can pass an array of IDs and also select specific columns? 🚀

```php
<?php
// You can pass an array of ids, an select specific columns
User::find(id: [1, 2], columns: ['email']);
// select `email` from `users` where `users`.`id` in (1, 2)
```

## Laravel Tip 💡: Load Relationship Count on the Fly ([⬆️](#eloquent--database-tips-cd-))

When working with models, you might need the count of a relationship. If you forget to eager load it, you can always use "loadCount" to load the count on the fly 🚀

```php
<?php
$user = User::first();

// Load the count of related posts on the fly
$user->loadCount('posts');

// You can even constraint it
$user->loadCount('posts', fn(Builder $query) => $query->whereNull('published'));

// Access the count via <relationship>_count
$user->posts_count
```

## Laravel Tip 💡: Move Column to First Position ([⬆️](#eloquent--database-tips-cd-))

>[!NOTE]
>Altering the structure of a populated table might cause downtime, depending on the number of records it has.

Did you know you can move a column to the first position in your table, even if it was added later on? Use the "first()" method to do that 🚀

```php
<?php

Schema::table('posts', function (Blueprint $table) {
    $table->string('uuid')->first();
});
```

## Laravel Tip 💡: Latest of Many ([⬆️](#eloquent--database-tips-cd-))

Have you ever needed to get the latest record from a one to many relationship? While you can use subqueries to do this, Laravel already ship with the "latestOfMany" method to do exactly that 🚀

```php
<?php

class User extends Model
{
    public function latestOrder()
    {
        return $this->hasOne(Order::class)->latestOfMany('created_at');
    }
}

// You can now get the latest order
$latestOrder = $user->latestOrder;

// It can also be eager loaded
$users = User::with('latestOrder')->get();
```

> You can find a practical use case, an alternative method, and a comparison between them [here](https://blog.oussama-mater.tech/laravel-eager-loading-is-bad).

## Laravel Tip 💡: A Cleaner Eager Loading Syntax ([⬆️](#eloquent--database-tips-cd-))

Sometimes, when need to eager load nested relationships, and for that we the use dot notation. But did you know you can also pass nested arrays? 🚀

```php
<?php

// Instead of this
$books = Book::with([
    'author.contacts',
    'author.publisher'
])->get();

// You can pass a nested array
$books = Book::with([
    'author' => [
        'contacts',
        'publisher'
    ]
])->get();
```

## Laravel Tip 💡: The "insertGetId" Method ([⬆️](#eloquent--database-tips-cd-))

Have you ever found yourself needing the ID of a newly inserted row? Laravel ships with the "insertGetId" method to do exactly that 🚀

```php
<?php

$id = DB::table('users')->insertGetId(
    ['email' => 'john@example.com', 'votes' => 0]
);

dd($id); // The ID of the newly inserted row
```

## Laravel Tip 💡: The "ddRawSql" Method ([⬆️](#eloquent--database-tips-cd-))

When debugging queries, we often use "dd()" or "toSql()", but did you know you can use "ddRawSql" to get the raw SQL with all bindings substituted? 🚀

```php
<?php

DB::table('users')->where('votes', '>', 100)->ddRawSql();
// "select * from `users` where `votes` > 100"
```

## Laravel Tip 💡: Avoid Duplicate Queries ([⬆️](#eloquent--database-tips-cd-))

We often eager load relationships manually using the "load" method. While this works, it can result in duplicate queries when the relationship is already loaded. This can be avoided by using the 'loadMissing' method 🚀

```php
<?php

// If the relationships are already loaded, this will result in duplicate queries
$users->load(['comments', 'posts']);

// This will not query the DB if the relationships are already there
$users->loadMissing(['comments', 'posts']);
```

## Laravel Tip 💡: The New "CollectedBy" Attribute ([⬆️](#eloquent--database-tips-cd-))

As of Laravel v11.28, instead of overriding the "newCollection" method, you can now use the new "CollectedBy" attribute to specify a custom collection for your model 🚀

```php
<?php

use Illuminate\Database\Eloquent\Attributes\CollectedBy;

#[CollectedBy(PostCollection::class)]
class Post
{
    public function newCollection(array $models = [])
    {
        return new PostCollection($models);
    }
}
```

## Laravel Tip 💡: Aggregate Functions ([⬆️](#eloquent--database-tips-cd-))

We often use "withCount" when working with relationships, but did you know other aggregate functions are available out of the box? For example, you can also use "sum", "min", and "max" functions 🚀

```php
<?php

Post::withSum('comments', 'votes')->first(); // $post->comments_sum_votes

Post::withMax('comments', 'votes')->first(); // $post->comments_max_votes

Post::withAvg('comments', 'votes')->first(); // $post->comments_avg_votes

Post::withMin('comments', 'votes')->first(); // $post->comments_min_votes

Post::withExists('comments')->first(); // $post->comments_exists_votes
```

## Laravel Tip 💡: The "toggle" method ([⬆️](#eloquent--database-tips-cd-))

At some point, we all needed to toggle a value, for example, a like feature that switches between states. While you can do it manually, Laravel ships with a "toggle" method to do exactly that 🚀

```php
<?php

// Instead of this 😑
if ($user->likes()->where('tweet_id', $tweet->id)->exists()) {
    $user->likes()->detach($tweet->id);
} else {
    $user->likes()->attach($tweet->id);
}

// You can do this 🔥
$user->likes()->toggle($tweet->id);

// It also works with multiple IDs
$user->products()->toggle([1, 2, 3]);
```

## Laravel Tip 💡: Get the Full Query Log ([⬆️](#eloquent--database-tips-cd-))

Ever needed to dump the full query log executed in a method? You can enable the query log at the very beginning and dump it at the end by using "enableQueryLog" and "getRawQueryLog" 🚀

```php
<?php

use Illuminate\Support\Facades\DB;

DB::enableQueryLog();

User::whereNotNull('email_verified_at')->get();

DB::getRawQueryLog();
// select * from `users` where `email_verified_at` is not null
// time: 0.33
```

## Laravel Tip 💡: The New "rawColumn" Method ([⬆️](#eloquent--database-tips-cd-))

Laravel v11.32 introduces a new "rawColumn" method. Now, instead of having to use a DB statement when the grammar does not support updating or creating the column, you can use the "rawColumn" method 🚀

```php
<?php

new class extends Migration {
    public function up()
    {
        // Instead of this
        Schema::create('posts', function (Blueprint $table) {
            $table->id();
        });

        DB::statement('alter table `posts` add `legacy_boolean` int(1) default 0 not null');

        Schema::table('posts', function (Blueprint $table) {
            $table->index(['id', 'legacy_boolean']);
        });

        // You can now do this
        Schema::create('table', function (Blueprint $table) {
            $table->id();
            $table->rawColumn('legacy_boolean', 'int(1)')->default(0);
            $table->index(['id', 'legacy_boolean']);
        });
    }
};
```

## Laravel Tip 💡: Explain Eloquent Queries ([⬆️](#eloquent--database-tips-cd-))

Have you ever needed to run an EXPLAIN on an Eloquent query to check if an index is being used? While you could manually extract the raw query and run EXPLAIN on it, you can just chain the "explain" method to do exactly that 🚀

```php
<?php

User::query()
    ->where('email', 'john@example.com')
    ->explain()
    ->dd();

array:1 [
  0 => {#3368
    +"id": 1
    +"select_type": "SIMPLE"
    +"table": null
    +"partitions": null
    +"type": null
    +"possible_keys": null
    +"key": null
    +"key_len": null
    +"ref": null
    +"rows": null
    +"filtered": null
    +"Extra": "no matching row in const table"
  }
]
```

## Laravel Tip 💡: The "firstOrNew" Method ([⬆️](#eloquent--database-tips-cd-))

Sometimes you may want to check if a model exists, and if not, instantiate it without saving it to the database right away. Laravel ships with the "firstOrNew" to do exactly that 🚀

```php
<?php

use App\Models\User;

// Find the user by email, or save it to the database if it doesn't exist
User::firstOrCreate(['email' => 'name@example.com']);

// Find the user by email, or instantiate a new User instance without saving it
User::firstOrNew(['email' => 'name@example.com']);

// Do something with $user

// Save it to the database
$user->save();
```

## Laravel Tip 💡: The "withWhereHas" Method ([⬆️](#eloquent--database-tips-cd-))

Have you ever needed to eager load a relationship but also constrain it with relationship existence? While you can do that manually with 2 methods, Laravel ships with the "withWhereHas" method to do exactly that 🚀

```php
// Instead of this
User::query()
    ->whereHas('posts', fn (Builder $query) => $query->where('featured', true))
    ->with(['posts' => fn (Builder $query) => $query->where('featured', true)])
    ->get();

// You can simply use withWhereHas 🔥
User::query()
    ->withWhereHas('posts', fn (Builder $query) => $query->where('featured', true))
    ->get();

// This will retrieve all users that meet the condition, along with only their featured posts.
```

## Laravel Tip 💡: Update Pivot Columns ([⬆️](#eloquent--database-tips-cd-))

Have you ever needed to update a pivot column? While you can manually handle this with the query builder, Laravel ships with the "updateExistingPivot" method to do exactly that 🚀

```php
<?php

$user = User::first();
$roleId = Role::value('id');

$user->roles()->updateExistingPivot($roleId, [
    'active' => false,
]);

// UPDATE `role_user` SET `active` = 0 WHERE `role_user`.`user_id` = 1 AND `role_id` IN (1)
```

## Laravel Tip 💡: Prevent Accessing Missing Attributes ([⬆️](#eloquent--database-tips-cd-))

Did you know you can configure Laravel to throw an exception when attempting to access a missing attribute? This is useful during development to catch typos or changes in the table structure 🚀

```php
<?php

use Illuminate\Database\Eloquent\Model;

Model::preventAccessingMissingAttributes(! app()->isProduction());

$user = User::select('name')->first();
$user->email // throws a `MissingAttributeException` exception
```

## Laravel Tip 💡: The New "incrementOrCreate" Method ([⬆️](#eloquent--database-tips-cd-))

As of Laravel v11.39.1, a new "incrementOrCreate" method has been introduced. It allows you to create a record if it does not exist or increment the specified column otherwise 🚀

```php
<?php

PromoCodeUsage::incrementOrCreate(
    attributes: ['code' => 'oussama-25-off'], // Thats a valid code for JetBrains products 🔥
    column: 'usage_count', // Column to increment
    default: 1, // Default value if the record doesn't exist
    step: 1, // Increment step
    extra: ['last_used_at' => now()] // Additional data to update
);
```

## Laravel Tip 💡: Keep an Eye on Open Connections ([⬆️](#eloquent--database-tips-cd-))

Did you know that Laravel 9.24 and upwards ships with the db:monitor command? This command allows you to keep an eye on how many open connections you have and react if you exceed a threshold 🚀

```php
<?php

use Illuminate\Database\Events\DatabaseBusy;
use Illuminate\Support\Facades\Event;

public function boot(): void
{
    Event::listen(function (DatabaseBusy $event) {
        // Send a notification
    });
}

// Schedule a cron job to run the following command every minute.
// If the number of open connections exceeds 100, the DatabaseBusy event will be triggered,
// allowing you to send a notification to the team.
php artisan db:monitor --databases=mysql --max=100
```

## Laravel Tip 💡: The "MassPrunable" trait ([⬆️](#eloquent--database-tips-cd-))

If you are pruning models with the "Prunable" trait and not using model events, you might as well use the "MassPrunable" trait to prune them with a single query. This will be much more efficient 🚀

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\MassPrunable;

class Flight extends Model
{
    use MassPrunable;

    public function prunable(): Builder
    {
        return static::where('created_at', '<=', now()->subMonth());
    }
}

// Schedule the pruning command to run daily for example
$schedule->command(PruneCommand::class)->daily();
```

## Laravel Tip 💡: Restore Trashed Models ([⬆️](#eloquent--database-tips-cd-))

Have you ever needed to restore trashed models? While you could do this manually, Laravel ships with a restore method for exactly this 🚀

```php
<?php

Flight::query()
    ->onlyTrashed() // Only the trashed records will be targeted
    ->where('airline_id', 1)
    // ->update(['deleted_at' => null]) Instead of this
    ->restore(); // You can do this 🔥
    
// Restores all trashed records matching the condition with a single query 🔥
```

## Laravel Tip 💡: Bootable Traits ([⬆️](#eloquent--database-tips-cd-))

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

## Laravel Tip 💡: Boot Traits with Attributes ([⬆️](#eloquent--database-tips-cd-))

![Laravel](https://img.shields.io/badge/Laravel-%3E%3D12.22-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)

Laravel [bootable traits](#laravel-tip--bootable-traits-️) are great for extracting logic, but they come with a strict naming convention. Since Laravel v12.22, you can use proper PHP attributes, which not only makes the code cleaner but also lets you choose method names freely 🚀

```php
<?php

use Illuminate\Database\Eloquent\Attributes\Boot;
use Illuminate\Database\Eloquent\Attributes\Initialize;

// Instead of using boot[TraitName] and initialize[TraitName],
// you can now use attributes and give your methods readable names 🔥

trait HasToken
{
    #[Boot]
    public static function bootHasToken()
    {
        //
    }

    #[Initialize]
    public function initializeHasToken()
    {
        //
    }
}
```

## Laravel Tip 💡: The New "whereAttachedTo" Method ([⬆️](#eloquent--database-tips-cd-))

We have all used "whereHas", and sometimes you need to constrain it to match specific models. Since Laravel v12.13, you can use "whereAttachedTo" for exactly that 🚀

```php
<?php

$tags = Tag::where('created_at', '>', now()->subMonth())->get();

// instead of this 🥱
Post::whereHas('tags', function (Builder $query) use ($tags) {
    $query->whereKey($tags);
})->get();

// You can do this 🔥
Post::whereAttachedTo($tags)->get();
```
