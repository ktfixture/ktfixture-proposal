# Template Defination

* **Type**: Design proposal
* **Author**: Vinicius Moleta, Tiarê Balbi
* **Status**: In Review
* **Prototype**: To Do

## Use cases
* Define one or more templates for a specific type to describe different usage scenarios;
* Usage of a specific template for a specific type in a test case.

## Description
Templates are a definition of a data structure to a specific model allowing you to create multiple combinations of data.

```
Fixture.define<Client> {
    template { "valid-user-template", {
        using("name" withValue "John")
        using("age" withValue 18..100)
        using("address" using Fixture.with<Address>("valid-address-template")
    }}

    template { "invalid-user-template", {
        copying {"valid-user-template", {
            field("name" withValue "Brian")
        }}
    })
}
```




