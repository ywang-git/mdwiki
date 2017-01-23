# Introduction to Architecting Systems for Scale

## Load Balancing: Scalability & Redundancy

### Smart Clients

### Hardware Load Balancers

### Software Load Balancers

## Caching

> It also ensures you don't optimize access patterns which can't be replicated with your caching mechanism or access patterns where performance becomes unimportant after the addtion of caching.

### Application Versus Database Caching

> read-through cache

### In Memory Caches

### Content Distribution Networks

### Cache Invalidation

> each time a value changes, write the new value into the cache (this is called a write-through cache) or simply delete the current value from the cache and allow a read-through cache to populate it later (choosing between read and write through caches depends on your application's details, but generally I prefer write-through caches as they reduce likelihood of a stamped on your backend database).

> e.g. if you are trying to add application level caching in-front of a full-text search engine like SOLR)

> e.g. instead of DELETE FROM a WHERE ..., retrieve all the items which match the criteria, invalidate the corresponding cache rows and then delete the rows by their primary key explicitly

## Off-Line Processing
### Message Queues
> your web applications to quickly publish messages to the queue, and have other consumers processes perform the processing outside the scope and timeline of the client request.

> Slicehost

> that they allow you to create a separate machine pool for performing off-line processing rather than burdening your web application servers. This allows you to target increases in resources to your current performance or throughput bottleneck rather than uniformly increasing resources across the bottleneck and non-bottleneck systems.

### Scheduling Periodic Tasks
> a problem waiting for a widely accepted solution which easily supports redundancy

> a Puppet config

### Map-Reduce
> SQL database, but that approach may not scale up trivially once the quantity of data stored or write-load requires sharding your database, and will usually require dedicated slaves for the purpose of performing these queries

## Platform Layer
> such that your web applications communicate with a platform layer which in turn communicates with your databases

> First, separating the platform and web application allow you to scale the pieces independently

> Second, adding a platform layer can be a way to reuse your infrastructure for multiple products or interfaces (a web application, an API, an iPhone app, etc.) without writing too much redundant boilerplate code for dealing with caches, databases, etc.

> Third, a sometimes underappreciated aspect of platform layers is that they make it easier to scale an organization.

