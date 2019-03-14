This is a living document containing the Nexmo API standards. We'll be discussing
new standards in #api-standards on Slack, so please join us if you're interested
in contributing.

## Open API Spec

We document APIs using [Open API 3.0](https://swagger.io/docs/specification/about/)
 (formerly known as Swagger). These documents live in the
[API Specification](https://github.com/nexmo/api-specification) repo.

## General API Guidelines

> These are general API guidelines that I haven't found a home for yet

* Updating resources will fail if required parameters are not set.
* Unsent optional parameters will not be overwritten with default values.
* Response for a POST or GET will be the same resource.
* All APIs that allow updating a resource will also allow fetching a resource.
* In each context properties that are always unknown may be omitted. For example: a request to sending an SMS never contains DLR data.
* Properties that are potentially unknown should be included, but without a value. For example, if the Cloud Communications Platform cannot call the phone number defined in a request from Call API, the return properties will not have a valid `call_start` and `call_end`.
