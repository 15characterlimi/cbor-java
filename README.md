cbor-java
=========

A Java 7 implementation of [RFC 7049](http://tools.ietf.org/html/rfc7049): Concise Binary Object Representation ([CBOR](http://cbor.io/))


[![Build Status](https://img.shields.io/travis/c-rack/cbor-java.svg?branch=master&style=flat)](https://travis-ci.org/c-rack/cbor-java)
[![Coverage Status](http://img.shields.io/coveralls/c-rack/cbor-java/master.svg?style=flat)](https://coveralls.io/r/c-rack/cbor-java?branch=master)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/1218/badge.svg)](https://scan.coverity.com/projects/1218)
[![Dependency Status](https://www.versioneye.com/user/projects/555e2fb6634daa30fb000ea0/badge.svg?style=flat)](https://www.versioneye.com/user/projects/555e2fb6634daa30fb000ea0)


## Features

* Encodes and decodes **all examples** described in RFC 7049
* Provides a **fluent interface builder** for CBOR messages
* Supports semantic tags
* Supports 64-bit integer values
* Passes all [CPD](http://c-rack.github.io/cbor-java/cpd.html), [PMD](http://c-rack.github.io/cbor-java/pmd.html) and [FindBugs](http://c-rack.github.io/cbor-java/findbugs.html) tests

## Documentation

* [Documentation](http://c-rack.github.io/cbor-java/)
* [JavaDoc](http://c-rack.github.io/cbor-java/apidocs/index.html)

## Maven Dependency

Add this to the dependencies section of your pom.xml file:

```xml
<dependency>
    <groupId>co.nstant.in</groupId>
    <artifactId>cbor</artifactId>
    <version>0.5</version>
</dependency>
```

## Usage

### Encoding Example

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
CborEncoder encoder = new CborEncoder(baos);
encoder.encode(new CborBuilder()
    .add("text")                // add string
    .add(1234)                  // add integer
    .add(new byte[] { 0x10 })   // add byte array
    .addArray()                 // add array
        .add(1)
        .add("text")
        .end()
    .build());
byte[] encodedBytes = baos.toByteArray();
```

### Decoding Example

```java
ByteArrayInputStream bais = new ByteArrayInputStream(encodedBytes);
CborDecoder decoder = new CborDecoder(bais);
List<DataItem> dataItems = decoder.decode();
for(DataItem dataItem : dataItems) {
    // process data item
}
```

### Streaming Decoding Example

```java
ByteArrayInputStream bais = new ByteArrayInputStream(encodedBytes);
CborDecoder decoder = new CborDecoder(bais);
decoder.decode(new DataItemListener() {

    @Override
    public void onDataItem(DataItem dataItem) {
        // process data item
    }

});
```

## Contribution Process

This project uses the [C4 process](http://rfc.zeromq.org/spec:16) for all code changes.

> "Everyone, without distinction or discrimination, SHALL have an equal right to become a Contributor under the
terms of this contract."

## License

Copyright 2013-2015 Constantin Rack

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
