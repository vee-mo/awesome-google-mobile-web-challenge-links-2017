# Lesson 3: Service Workers

[<= GO BACK ](../README.md)

If some of the topics in lesson 3 were new to you, we hope the resource links here will help you:


## Resource Links

* [Firefox: Service Workers (explained)](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)
* [Google Web Fundamentals: Overview](https://developers.google.com/web/fundamentals/primers/service-workers)
* [Google Web Fundamentals: Service Workers Life Cycle](https://developers.google.com/web/fundamentals/primers/service-workers/lifecycle)
* [Firefox: Cache](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
* [Firefox: Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
* [High-performance service worker loading] (https://developers.google.com/web/fundamentals/primers/service-workers/high-performance-loading)


## Overview:
The service worker handles the requests the user makes. It can send the request straight to the server (cloud) or first try to load cached data while requesting new data from the server. 

![service worker](https://www.smashingmagazine.com/wp-content/uploads/2016/11/service-worker-offline-large-opt.jpg)


## Creating cache and saving information in the cache:

```
caches.open(‘cache_store_name’).then(function(cache) {
    return cache.addAll(urlsToCache);
})
```

It is possible to use these 3 ways to store information in cache:

* cache.add(request): stores single request
* cache.addAll(request): stores an array of requests
* cache.put(request, response): stores a single request and its response


## Fetch cached data and non-cached data

```
caches.match(event.request).then(function(response) {
    return response || fetch(event.request);
})
```

It is possible to use these 2 ways to fetch cached data:

* caches.match(cache_name): Matches a single request and return a promise
* caches.matchAll(cache_name): Matches an array and returns a promise


## Delete Cache

```
caches.keys().then(function(cacheNames) {
    return Promise.all(
    cacheNames.filter(function(cacheName) {
        return cacheName.startsWith('wittr-') && cacheName != static_cache_name;
        }).map(function(cacheName) {
            return caches.delete(cacheName);
        })
    );
})
```

* caches.delete(cache_name): finds cache with given name and return a promise
* caches.keys(): returns a promise with an array of cache keys

