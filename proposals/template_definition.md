# Template Definition

* **Type**: Design proposal
* **Author**: Vinicius Moleta, Tiarê Balbi
* **Status**: In Review
* **Prototype**: To Do

## Use cases
* Define one or more templates for a specific type to describe different usage scenarios
* Template re-usage
* Template customization with actions such as using (inserting or replacing a property value) and excluding(removing property from the template)

## Description
Templates are a definition of a data structure to a specific model allowing you to create multiple combinations of data.

***Actions:***
* ***using***: Define a field value in the template
* ***copying***: Copy a full template definition allowing you override the properties defined in the previous template


```
Fixture.define<Client> {
    template { "valid-user-template", {
        using("name" withValue "John")
        using("age" withValue 18..100)
        using("address" from Fixture.with<Address>("valid-address-template")
    }}

    template { "invalid-user-template", {
        copying {"valid-user-template", {
            using("name" withValue "Brian")
        }}
    })
}
```
