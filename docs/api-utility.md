## 缓存

Gets or, when options are provided, sets the limits of _libvips'_ operation cache.
Existing entries in the cache will be trimmed after any change in limits.
This method always **返回** cache statistics,
useful for determining how much working memory is required for a particular task.

**参数**

-   `options` **([Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) \| [Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean))** Object with the following attributes, or Boolean where true uses default cache settings and false removes all caching (optional, default `true`)
    -   `options.memory` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** is the maximum memory in MB to use for this cache (optional, default `50`)
    -   `options.files` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** is the maximum number of files to hold open (optional, default `20`)
    -   `options.items` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** is the maximum number of operations to cache (optional, default `100`)

**实例**

```javascript
const stats = sharp.cache();
```

```javascript
sharp.cache( { items: 200 } );
sharp.cache( { files: 0 } );
sharp.cache(false);
```

**返回** **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 

## 并发性

Gets or, when a concurrency is provided, sets
the number of threads _libvips'_ should create to process each image.
The default value is the number of CPU cores.
A value of `0` will reset to this default.

The maximum number of images that can be processed in parallel
is limited by libuv's `UV_THREADPOOL_SIZE` environment variable.

This method always **返回** the current concurrency.

**参数**

-   `concurrency` **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)?** 

**示例**

```javascript
const threads = sharp.concurrency(); // 4
sharp.concurrency(2); // 2
sharp.concurrency(0); // 4
```

**返回** **[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)** concurrency

## 计数器

Provides access to internal task counters.

-   queue is the number of tasks this module has queued waiting for _libuv_ to provide a worker thread from its pool.
-   process is the number of resize tasks currently being processed.

**示例**

```javascript
const counters = sharp.counters(); // { queue: 2, process: 4 }
```

**返回** **[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)** 

## simd

Get and set use of SIMD vector unit instructions.
Requires libvips to have been compiled with liborc support.

Improves the performance of `resize`, `blur` and `sharpen` operations
by taking advantage of the SIMD vector unit of the CPU, e.g. Intel SSE and ARM NEON.

This feature is currently off by default but future versions may reverse this.
Versions of liborc prior to 0.4.25 are known to segfault under heavy load.

**参数**

-   `simd` **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)**  (optional, default `false`)

**示例**

```javascript
const simd = sharp.simd();
// simd is `true` if SIMD is currently enabled
```

```javascript
const simd = sharp.simd(true);
// attempts to enable the use of SIMD, returning true if available
```

**返回** **[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)** 
