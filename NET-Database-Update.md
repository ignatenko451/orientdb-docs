---
search:
   keywords: ['NET', 'c#', 'ODatabase', 'update']
---

# OrientDB-NET - `Update()`

This method creates an `OsqlUpdate` object, which you can use in modifying data on the database.

## Updating Records

### Syntax

```
// UPDATING RECORDS
OSqlUpdate Update()
```

There are several methods available to the `OSqlUpdate` method.  These allow you to build and execute the update against your database.


#### Defining the Target

When using this method, you can update by class, cluster or Record ID.

- **Class Updates**

  ```
  OSqlUpdate database.Update()
     .Class(string <class-name>)
  ```

- **Cluster Updates**

  ```
  OSqlUpdate database.Update()
     .Cluster(string <cluster-name>
  ```

- **Record Updates**

  ```
  // RECORD METHOD
  OSqlUpdate database.Update()
     .Record(ORID <record-id>)

  // RECORD ARGUMENT
  OSqlUpdate database.Update(ORID <record-id>)
  ```

For the sake of simplicity, syntax cases shown hereafter assume that you're updating a class.

#### Defining the Update

When using this method, you have a few options in defining the update that you want to make: whether you're adding or removing data, or changing records.

- **Setting Field**

  ```
  OSqlUpdate database.Update(<rid>)
     .Set(<field>, <value>)
  ```

- **Adding Fields**

  ```
  OSqlUpdate database.Update(<rid>)
     .Add(<field>, <value>)
  ```

- **Removing Fields**

  ```
  OSqlUpdate database.Update(<rid>)
     .Remove(<field>)
  ```

#### Executing Updates

Using the above methods you can build the update that you want, however OrientDB-NET does not execute the update on your database until you use an execution method: 

- `Run()` Executes the update on the database and returns an integer.

- `ToString()` Executes the update on the database and returns a string.


### Example

For instance, say that you have an accounting application written in C#/.NET.  For your accounts, you have a region dedicated the Eastern United States.  However, business has been going so well that you want to break the Northeast off into its own region.  You build an array of states in the Northeast, then run the following update:

```csharp
foreach(string state in ne_states)
{
   int accountUpdate = database.Update()
      .Class("Account")
      .Set("region", "US-Northeast")
      .Where("region").Equals("US-East")
      .And("state").Equals(state)
      .Run();
}   
```


