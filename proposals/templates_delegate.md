# Template - Using delegates

* **Type**: Design proposal
* **Author**: Vinicius Moleta, Tiarê Balbi
* **Status**: In Review
* **Prototype**: To Do

## Use cases
* Should allow us to define a new property in your class using delegate and a template name;
* Should allow us to use action before creating the instances.

## Description
Allow usage of delegate pattern to create test data in your class.

## Examples

```
private val client: Client by Fixture.single("valid") {
    using("name" withValue "John {index}")
    excluding(["age"])
}

private val clients: List<Client> by Fixture.multiple(5, "valid") {
    using("name" withValue "John")
    excluding(["age"])
}
```
