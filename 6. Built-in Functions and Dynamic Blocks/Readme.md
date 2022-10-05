### Built-in Functions and Dynamic Blocks
- Terraform Built in Functions
- Terraform Type Constraints
- Terraform Dynamic Blocks

## Terraform Built in Functions
- User defined functions are not allowed, only built-in ones (eg: join, max, timestamp(), contains)
- We can use thse functions inside various places in our terraform code for eg: resource and data resource block, provisioners, variables.
![image](https://user-images.githubusercontent.com/76193921/193986546-7d23a4d6-a158-491d-a17b-319a092914fb.png)

- We can test out the buil in funcion using <b>terraform console</b> command.


## Terraform Type Constraints
- Type constraints control the type of variable values you can pass to your terraform code.
- Primitive (number, string, bool) and Complex(multiple types in a single variable){list, tuple, map, object}
- Complex are of two types : </br>
- 1) Collections </br>
- 2) Structual</br>

#### Collections : type allows multiple values of one primitive types to be grouped together
- Constructors for these collections include :  
        - list(type) </br>
        -  map(type) </br>
        -  set(type) </br>
      
 ![image](https://user-images.githubusercontent.com/76193921/193987739-c7807a98-89c6-47ba-b06d-3ab4583fccfe.png)


### Structural : type allow smultiple values of different primitive type to be grouped together
- Constructors for these collections include :  
        - object(type) </br>
        -  tuple(type) </br>
        -  set(type) </br>
 
 ![image](https://user-images.githubusercontent.com/76193921/193988005-9796dad5-b63f-41e8-8e8c-bd97cd43f0db.png)

### ANY CONSTRAINT : is a placeholder for a primitive type yet to be decided
- Actual type will be determined at runtime
 ```
 variable "data" {
      type = list(any)
      default = [1, 2, 3, 4]
   }
 ```
 
 ## Terraform Dynamic Blocks
 - Dynamically constructs repeatable nested configuration blocks inside terraform resources
 - supported with the following block types:
 - 1) resources
 - 2) data
 - 3) provider
 - 4) provisioner
![image](https://user-images.githubusercontent.com/76193921/193988946-2c17ac29-62b5-41e8-b2e5-3c03795caddb.png)

![image](https://user-images.githubusercontent.com/76193921/193988898-9d53fb95-17ab-488d-9647-bd0ee12c7d41.png)

- the dynamic block expects a complexd vatiable type to iterate over
- it acts like a for loop and outputs a nested block for each element in our variable
- Makes code look cleaner
- Only use dynamic blocks when you need to hide details in order to build a cleaner user interface when writing reusable modules
- not ot overuse dynamic blocks in your main code, as they can be hard to read and mantain

![image](https://user-images.githubusercontent.com/76193921/193989251-e95ae9f2-ce53-4598-9d8a-823201b8dab7.png)
