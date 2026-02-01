## Chap4 - Variables

### defining variables
- To define variable in `varibales.tf`, if we dont mention default value, we will be prompted when running `terraform apply`
```
varibale "filename" {
    default = "/etc/host.txt"
}
```
- To reference;
```
var.filename
```
- we can also use `-var "filename=/etc/host.txt"` flag while running terraform commands. Environmental variables like `TF_VAR_filename="/etc/host.txt"`
- we can define all varibales in varibales definition files. `*.tfvars, *.tfvars.json, *.auto.tfvars, *.auto.tfvars.json`. 
- If using variable definiton files, we have to mention it like `terraform apply -var-file *.tfvars`.
- variable precedence in terraform. `-var or -var-file` has the highest precedence.
![alt text](image.png)

### using variables
![alt text](image-1.png)

`sensitive` if true, variables will only be recorded in statefile and supressed during terraform operations.

### validation rules for input variables
we can add validation block for input variables, i.e,
![alt text](image-2.png)

variable types are `string | number | bool | any (default)`
typeconversion can be happened from bool to string (vice versa), string to number (viceversa). Below example, typeconversion is not possible.
![alt text](image-3.png)

**list** type![alt text](image-4.png)
**list of a type**![alt text](image-6.png)

**map**
![alt text](image-5.png)
**map of a type**![alt text](image-7.png)

**Sets**: Like list but cant have duplicated values.
![alt text](image-8.png)

**objects**
![alt text](image-9.png)

**tuple**: List of different types
![alt text](image-10.png)

### Output variables
![alt text](image-11.png)
- `terraform output`command to display output.

![alt text](image-12.png)