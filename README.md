#  Java Uuid Generator (JUG)

JUG is a set of Java classes for working with UUIDs: generating UUIDs using any of standard methods, outputting
efficiently, sorting and so on.
It generates UUIDs according to the [UUID specification (RFC-4122)](https://tools.ietf.org/html/rfc4122)
(also see [Wikipedia UUID page](http://en.wikipedia.org/wiki/UUID) for more explanation)

JUG was written by Tatu Saloranta (<tatu.saloranta@iki.fi>) in 2002 (or so?), and has been updated over years.
In addition, many other individuals have helped fix bugs and implement new features: please see CREDITS for the complete list.

Jug licensing is explained in file LICENSE; basically you have a choice of one of 2 common Open Source licenses (when downloading source package) -- Apache License 2.0 or GNU LGPL 2.1 -- and you will need to accept terms for one of the license.
Please read LICENSE to understand requirements of the license you choose.

## Usage

JUG can be used as a command-line tool (via class 'com.fasterxml.uuid.Jug`), or as a pluggable component.
Maven coordinates are:

    <dependency>
      <groupId>com.fasterxml.uuid</groupId>
      <artifactId>java-uuid-generator</artifactId>
      <version>3.1.3</version>
    </dependency>


## Known Issues

JDK's `java.util.UUID` has flawed implementation of `compareTo()`, which uses naive comparison
of 64-bit values. This does NOT work as expected, given that underlying content is for all purposes
unsigned. For example two UUIDs:

```
7f905a0b-bb6e-11e3-9e8f-000000000000
8028f08c-bb6e-11e3-9e8f-000000000000
```

would be ordered with second one first, due to sign extension (second value is considered to
be negative, and hence "smaller").

Because of this, you should always use external comparator, such as
`com.fasterxml.uuid.UUIDComparator`, which implements expected sorting order that is simple
unsigned sorting, which is also same as lexicographic (alphabetic) sorting of UUIDs (when
assuming uniform capitalization).

## Alternative JVM UUID generators

There are many other publicly available UUID generators. For example:

* [Apache Commons IO](http://commons.apache.org/sandbox/commons-id/uuid.html) has UUID generator
* [eaio-uuid](http://stephenc.github.io/eaio-uuid/)
* JDK has included `java.util.UUID` since 1.4, but omits generation methods (esp. time/location based ones), has sub-standard performance for many operations and implements comparison in useless way
* [ohannburkard.de UUID generator](http://johannburkard.de/software/uuid/)

