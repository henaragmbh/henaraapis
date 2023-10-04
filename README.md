# Henara APIs

This repository contains interface definitions of public Henara APIs that support gRPC or REST protocols. You can use these definitions to generate client libraries, documentation, and other artifacts.

## Repository Structure

This repository uses a directory hierarchy that reflects the Henara
API product structure. In general, every API has its own root
directory below the folder *henara/*. The proto package names match the directory names. This makes it
easy to locate the proto definitions and ensures that the generated
client libraries have idiomatic namespaces in most programming languages.

## Generate gRPC Source Code

To generate gRPC source code for APIs in this repository, you need to install both [Protocol Buffers](https://protobuf.dev) and [gRPC](https://grpc.io) on your local
machine, then you can use *protoc* to generate the source code. You need to integrate the generated source code or the generation steps into your applications build system.

In the given web-pages you might follow the tutorials for your preferred programming languages.

Integration of gRPC code generation is already provided for various development and build solutions.

## APIs
[Customer API](documentation/customer_api)


## API-Variants

Our APIs are usable in multiple technological variants.


### Variant 1 - direct gRPC

gRPC is great - it generates API clients and server stubs in many programming languages, is fast, easy to use, bandwidth efficient, and its design is battle-tested by Google.

We implement all our services exclusively with gRPC APIs. Other variants are made possible with the help of upstream proxies.

The direct use of gRPC is by nature the most efficient variant for API clients.

With the API definitions provided in this repo our customers can generate their client implementation.

The API definition contains both, the structural and the semantic documentation of the messages and their attributes.


### Variant 2 - gRPC-web via Envoy Proxy

gRPC uses HTTP2 as a transport protocol and cannot currently be used directly by browser clients due to a lack of sufficient support in the browser.

[gRPC-Web](https://grpc.io/docs/platforms/web) uses HTTP1.1, allowing browser-based clients to access gRPC APIs.

gRPC-Web clients connect to the gRPC service through a special proxy, which maps gRPC-Web to gRPC and is operated by us in parallel. A popular implementation for this purpose is [Envoy](https://www.envoyproxy.io).

gRPC-Web comes with a [JavaScript implementation](https://github.com/grpc/grpc-web) for browser clients ([example](https://grpc.io/docs/platforms/web/quickstart)).


### Variant 3 - RESTful via grpc-gateway

gRPC is great. However, you may still want to use a traditional RESTful JSON API.

The reasons can range from maintaining backwards compatibility, supporting languages ​​or clients not well supported by gRPC or to simply maintaining the aesthetics and tools of a RESTful JSON architecture.

[gRPC-Gateway](https://grpc-ecosystem.github.io/grpc-gateway) is a technology for generating proxies that map a gRPC API to a RESTful JSON API.

This generated proxy is operated by us in parallel.


#### OpenAPI

In addition to generating the proxy, gRPC-Gateway also provides a description of the interface in [OpenAPI](https://www.openapis.org) format.

Our customers can generate clients in various programming languages ​​using the OpenAPI interface description.

[This Docker image](https://hub.docker.com/r/openapitools/openapi-generator-cli) is widely used for this task.
