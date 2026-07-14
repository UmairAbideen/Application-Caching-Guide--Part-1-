# ⚡ Laravel 10 Application Caching Guide

This project demonstrates **Application Data Caching** techniques in **Laravel 10** to improve performance by reducing unnecessary database queries and serving frequently accessed data from cache.

The project covers:

- Laravel Cache
- Query Cache
- Redis Cache
- Cache Tags

> **Without Cache:** Every request hits the database.  
> **With Cache:** Frequently used data is served from cache, resulting in faster response times and lower database load.

---

# ❓ Why Use Application Caching?

Application caching is useful when:

- You want to reduce database queries.
- You need faster page loading.
- Frequently accessed data rarely changes.
- You want to improve application performance.
- Your application serves many concurrent users.

Examples:

- Product listings
- Categories
- User profiles
- Dashboard statistics
- API responses
- Application settings

Without caching, every user request executes the same database query repeatedly.

---

# 🧩 Caching Concepts Covered

✅ Laravel Cache

✅ Query Cache

✅ Redis Cache

✅ Cache Tags

---

# 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Laravel 10 | PHP Framework |
| Cache Facade | Data Caching |
| Eloquent ORM | Database Operations |
| Redis | High-Speed In-Memory Cache |
| MySQL | Database |

---

# 1️⃣ Laravel Cache

## What is Laravel Cache?

Laravel Cache stores frequently used application data so it doesn't need to be retrieved from the database every time.

Think:

> "Store it once, reuse it many times."

---

## Example

```php
use Illuminate\Support\Facades\Cache;

$products = Cache::remember('products', 60, function () {

    return Product::all();

});
```

Meaning:

- First request → Query database and store result.
- Next requests → Return cached data.

---

## Other Common Methods

Store data manually:

```php
Cache::put('users', User::all(), 60);
```

Retrieve data:

```php
Cache::get('users');
```

Remove cache:

```php
Cache::forget('users');
```

---

## When to Use Laravel Cache?

Use Laravel Cache when:

- ✅ Frequently accessed data
- ✅ Dashboard widgets
- ✅ Product listings
- ✅ Categories
- ✅ API responses

---

# 2️⃣ Query Cache

## What is Query Cache?

Query Cache stores the result of expensive database queries.

Instead of executing the same SQL query repeatedly, Laravel returns the cached result.

Think:

> "Run the query once, cache the result."

---

## Example

```php
$posts = Cache::remember('posts', 300, function () {

    return Post::latest()->get();

});
```

Instead of:

```
Database

↓

SELECT * FROM posts

↓

Return Results
```

Laravel does:

```
Database

↓

Store Result in Cache

↓

Return Cached Result
```

---

## When to Use Query Cache?

Use Query Cache when:

- ✅ Large product tables
- ✅ Reports
- ✅ Dashboard statistics
- ✅ Frequently viewed records

---

# 3️⃣ Redis Cache

## What is Redis Cache?

Redis is an **in-memory data store** used as Laravel's cache driver.

Instead of storing cache on disk, Redis stores everything in RAM, making it significantly faster.

Think:

> "Same cache, faster storage."

---

## Example

Configure Redis as the cache driver.

```
CACHE_DRIVER=redis
```

Laravel cache code remains the same.

```php
Cache::remember('products', 60, function () {

    return Product::all();

});
```

The only difference is that the cache is now stored in Redis.

---

## When to Use Redis Cache?

Use Redis when:

- ✅ Large applications
- ✅ High-traffic websites
- ✅ APIs
- ✅ E-commerce applications
- ✅ Real-time applications

---

# 4️⃣ Cache Tags

## What are Cache Tags?

Cache Tags group related cache entries together.

Instead of clearing the entire cache, you can clear only a specific group.

Think:

> "Organize cache into categories."

---

## Example

Store cache using tags.

```php
Cache::tags(['products'])->put('latest-products', Product::all(), 300);
```

Clear only product cache.

```php
Cache::tags(['products'])->flush();
```

Instead of deleting:

```
Everything
```

Laravel deletes only:

```
Products Cache
```

---

## When to Use Cache Tags?

Use Cache Tags when:

- ✅ Large applications
- ✅ Multiple cache groups
- ✅ Selective cache clearing
- ✅ Modular applications

Examples:

- Products
- Categories
- Users
- Orders

---

# ⚖️ Comparison

| Feature | Purpose | Best Used For |
|---------|---------|---------------|
| Laravel Cache | Cache application data | Products, Categories, API Data |
| Query Cache | Cache expensive database queries | Reports, Dashboards |
| Redis Cache | Store cache in memory (RAM) | High-performance applications |
| Cache Tags | Group related cache entries | Selective cache clearing |

---

# 🆚 When to Use What?

| Scenario | Recommended Technique |
|----------|-----------------------|
| Frequently accessed application data | Laravel Cache |
| Expensive database queries | Query Cache |
| High-traffic production applications | Redis Cache |
| Clear related cached data together | Cache Tags |

---

# 🔥 Real World Example

## E-Commerce Application

### Cached Data

```
Products

Categories

Brands

Featured Products

Dashboard Statistics
```

Application Flow:

```
User Requests Products

        │

        ▼

Check Cache

        │

   Cache Exists?

     │        │

    Yes      No

     │        │

Return     Query Database

Cached         │

Data           ▼

          Store in Cache

               │

               ▼

          Return Data
```

---

# 📦 Useful Laravel Commands

Clear Application Cache

```bash
php artisan cache:clear
```

Clear Configuration Cache

```bash
php artisan config:clear
```

Clear Route Cache

```bash
php artisan route:clear
```

Clear View Cache

```bash
php artisan view:clear
```

Optimize Application

```bash
php artisan optimize
```

Clear All Optimizations

```bash
php artisan optimize:clear
```

Run Development Server

```bash
php artisan serve
```

---

# 🎯 Key Takeaway

Laravel provides multiple ways to improve application performance through caching.

- **Laravel Cache** → Store frequently accessed application data.
- **Query Cache** → Cache expensive database query results.
- **Redis Cache** → Use Redis as a high-speed in-memory cache driver.
- **Cache Tags** → Organize and clear related cache entries efficiently.

Together, these techniques help build **fast, scalable, and high-performance Laravel applications** while reducing database load and improving response times.

---

## 📄 License

This project is open-source and available under the **MIT License**.
