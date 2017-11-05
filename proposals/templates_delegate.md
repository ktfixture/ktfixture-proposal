# Template - Using delegates

* **Type**: Design proposal
* **Author**: Vinicius Moleta, Tiarê Balbi
* **Status**: In Review
* **Prototype**: To Do

## Use cases
* Given a selected type of a desired property the delegate can provide you an object or a list of objects of the selected type by using a template and actions applied over the same template;
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
