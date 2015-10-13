# WLW Infrastructure
* Microservice Architecture
* 13 Applications/Services
* Communication over REST APIs and AMQP
* ~3K internal API request per minute
* One App owns it's data, fetching on the fly
* Search/ES is a place where data is aggregated

# Local Caching

## Benefits
* No HTTP request overhead for cached calls

## Drawbacks
* Each app implements it's own cache
* Cached data is duplicated in multiple caches
* Hard to invalidate all caches
* No monitoring e.g. on cache hit rates

# Proxy Caching
* Image of a transparent cache
* Why we choose varnish
* Free software under BSD license
* Well documented, free books, good documentation
* Easy to introduce, few code changes are needed
* Good expierience at e.g. at XING or OTTO

# Varnish features
* Reasonable default values
* Request aggregations when same request arrives multiple times
* Cache key construction
* Vary Header
* VCL configuration, everything is possible, we tried to come up with a set of simple rules
* Cache only json responses (not 500 html)
* response times went from 50-60ms from the fastest calls to ~7ms
* Expire header
* Grace time
* Cache invalidation: ban vs purge
* Plugins for Munin/NewRelic, CLI tools
* Code example API Server side
* Code example VCL

# Learnings
* purging a lot of cache entries with bans
* caching calls with very low hit rates
* expunging: When varnish RAM is too low, more calculation is used to free memory
* Try: Have a dedicated endpoint to varnish instead of sending the whole traffic through
 * better monitoring
 * slightly more implementation overhead
* When building a new API call you have varnish in your toolset
* Having fast APIs will has less impact than caching entire Pages
 * ESI looks intersting for that
