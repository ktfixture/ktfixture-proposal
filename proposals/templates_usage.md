# Template Usage

* **Type**: Design proposal
* **Author**: Vinicius Moleta, Tiarê Balbi
* **Status**: In Review
* **Prototype**: To Do

## Use cases
* Based on an object type and a template name I want to generate a list of object of that type;
* Allow you to re-use test data created to a specific model using different cases (template name);
* Allow you to customize a field in a pre-defined template;
* Be able to get a single object using a class type and the template name;
* Be able to get a list of objects using a class type and the template name;
* Customization of the generated data through actions such as "using" and "excluding".

## Description
The main goal in the usage of templates is to allow you re-use a pre-defined data model across your all your tests.

***Actions:***
* ***using***: allow you to override a field value in a template;
* ***excluding***: remove the field value from the template.

***Helpers:***
* _{index}_: Is a property that can be used in a value expression representing the index number,
if you fetch a single object the default value is 0.

***Notes:***
* Changes applied in the moment of fetching the data are not reflected in the original template;
* If you define/add a field to your template that is not present in the object your template will fail.

## Examples

```
@Test
fun `should create a single user` () {
  val client = Fixture.prepare<Client> {"template-name", {
        using("name" withValue "John {index}")
    }}.single()

  assertEquals("John 0", client.name)
}

@Test
fun `should not require defining the type in the method if the return is defined` () {
  val client: Client = Fixture.prepare {"template-name", {
        using("name" withValue "John {index}")
    }}.single()

  assertEquals("John 0", client.name)
}

@Test
fun `should create a list of client`() {
    val client: List<Client> = Fixture.prepare<Client> {"template-name", {
        using("name" withValue "John {index}")
    }}.multiple(5)

    assertEquals("John 0", client[0].name)
    assertEquals("John 1", client[1].name)
    assertEquals("John 2", client[2].name)
    assertEquals("John 3", client[3].name)
    assertEquals("John 4", client[4].name)
}

@Test
fun `should be able to re-use the definition to fetch multiple times`() {
    val definition = Fixture.prepare<Client> {"template-name", {
        using("name" withValue "John {index}")
    }}

    val client: Client = definition.single()
    assertEquals("John 0", client.name)

    val clients: List<Client> = definition.multiple(5)
    assertEquals("John 0", client[0].name)
    assertEquals("John 1", client[1].name)
    assertEquals("John 2", client[2].name)
    assertEquals("John 3", client[3].name)
    assertEquals("John 4", client[4].name)
}

```
