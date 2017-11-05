# Equality assertion

* **Type**: Design proposal
* **Author**: Vinicius Moleta, Tiarê Balbi
* **Status**: In Review
* **Prototype**: To Do

## Use cases
* Given a specific type T with templates defined, you can assert that all fields from two different objects of the same type T are the same;
* Before asserting all the fields from the expected and actual objects, you can apply actions on the expected object;
* If the assertion type is a list, all the actions and fields assertions will be applied to each object of the list.

## Description
Every time you want to assert equality on fields, you can use this feature to avoid writing multiple asserts to compare each field and to avoid copying the object changing the fields you expect to be different.

***Actions:***
 * ***using***: override a field value for the assertion;
 * ***excluding***: don't consider this field in the assertion.

***Notes:***
 * Assertion actions won't affect the objects being compared, only the assertion itself.

## Example
```
@Test
fun `assert operation result with expected value`() {
    val input: Client = Fixture.prepare { "template-name" {
      using("name" withValue "John from {address.city}")
    }}.single()

    val output: Client = Operation.resetAddress(input)

    Fixture.Assert.that(output).isEqualsTo(input) {
      using("name" withValue "John without address")
      excluding(["address"])
    }
}

@Test
fun `assert operation result with expected value as list`() {
    val input: List<Client> = Fixture.prepare<Client> { "template-name" {
      using("name" withValue "John {index} from {address.city}")
    }}.multiple(5)

    val output: List<Client> = Operation.resetAddress(input)

    Fixture.Assert.that(output).isEqualsTo(input) {
      using("name" withValue "John {index}")
      excluding(["address"])
    }
}
```
