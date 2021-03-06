# GeoIP Java API [![Build Status](https://travis-ci.org/maxmind/geoip-api-java.png?branch=master)](https://travis-ci.org/maxmind/geoip-api-java)

## Define Your Dependencies

We recommend installing this package with Maven. To do this, add the dependency to your pom.xml:

```xml
    <dependency>
        <groupId>com.maxmind.geoip</groupId>
        <artifactId>geoip-api</artifactId>
        <version>1.2.10</version>
    </dependency>
```

## Building Manually

### Installation
    mvn clean install

### Packaging
    mvn package

The jar file will be in the `target` directory.

### Testing
    mvn test

## API Changes

### 1.1.4

As of version 1.1.4 this API is thread safe.

### 1.1.0

IMPORTANT API Change for 1.1.x users: As of GeoIP 1.1.0 the
`lookupCountryXxxx` methods return `null` if a country can not be found. These
methods previously returned `--` or `N/A`. Be sure to check the return value
for `null`.


## Memory Caching and Other Options

The following options can be passed as the second parameter to the
`LookupService` constructor:

* `GEOIP_STANDARD` - Read database from file system. Uses the least memory.
* `GEOIP_MEMORY_CACHE` - Load database into memory. This provides faster
  performance but uses more memory
* `GEOIP_CHECK_CACHE` - Check for updated database.  If database has been
  updated, reload file handle and/or memory cache.
* `GEOIP_INDEX_CACHE` - Cache only the most frequently accessed index portion
   of the database, resulting in faster lookups than GEOIP_STANDARD, but less
   memory usage than `GEOIP_MEMORY_CACHE`. This is useful for larger
   databases such as GeoIP Organization and GeoIP City.  Note: for GeoIP
   Country, Region and Netspeed databases, `GEOIP_INDEX_CACHE` is equivalent
   to `GEOIP_MEMORY_CACHE`.

These options may be combined. For example:

```java
LookupService cl = new LookupService(dbfile, LookupService.GEOIP_MEMORY_CACHE | LookupService.GEOIP_CHECK_CACHE);
```
