## Chap 7
### count

`count` to define how many number of resources to be created inside of resource block.
```
variable "instance_count" {
  type    = number
  default = 3
}

resource "aws_instance" "web" {
  count         = var.instance_count
  ami           = "ami-0123456789abcdef0"
  instance_type = "t2.micro"

  tags = {
    Name = "web-${count.index}"
  }
}
```
![alt text](image.png)

If we remove one element from default list like this,
![alt text](image-1.png)

the result will look like this that last instance will be destroyed and forst two instances tags will be modified. Reason is the resources are created as a list. So, list always starts with index 0.
![alt text](image-2.png)

### for_each
for_each does not work with list. Variable type must be a set or map

![alt text](image-4.png)

Here, resources are created as maps than a list
![alt text](image-3.png)

If we now remove one instnace, only instance with that key will be removed
![alt text](image-5.png)

### Provisioners
Provisioners are used to run the commands on resources created. Mostly on vms or containers. The terraform (running locally or on a pipeline) should have access (authetication, security groups) to that resource to run commands on. Here, we are using `remote-exec` to run commands on remote resources. Provisioner blocks are executed after the resource has been created.
**Remote provisioner**
![alt text](image-6.png)

**Local Provisioner**
![alt text](image-7.png)

We can also run commands before the resource is destroyed.

Default failure behavior of provisioners is that terraform will throw the error and terraform apply command would fail and terraform rill consider the resource as tainted and will destroy it in next run.
![alt text](image-8.png)

If we want to continue executing terraform apply command, we need to add this condition `on_failure = continue`
![alt text](image-9.png)

*file is also a provisioner*

*Terraform recommends to use provisioners as last resort. We should consider using default options from provider to run any commands on resources created*
![alt text](image-10.png)

### Builtin functions
toset, file, length
![alt text](image-11.png)

Some other built-in functions: Numeric, string, collection, type conversion.
**Numeric** - max, min, ceil, floor
![alt text](image-12.png)

**String**
In `substr`, second argument is offset and third argument is length of string from offset
![alt text](image-13.png)

In `join` function, we join array elements into str.
![alt text](image-14.png)

**Collection**
- for sets, map and list
![alt text](image-15.png)

here, lookup fnc is used to get value of a specific key in a map
![alt text](image-16.png)
![alt text](image-17.png)

**Operators & Conditionals**
**Numeric Operators** - `+-/*`
**Equality operators** - `==`. `!=`, `8 != '8' -> true`
**Comparison operators** - `>, >=, <, >=`
**Logical operator** - `&&`, `||`, `! var.flag`

**condition**

![alt text](image-18.png)

To expan list or tuples for an function, we can use `expansion operator`
```
locals {
  numbers = [1, 2, 3]
}

output "result" {
  value = max(local.numbers...)  # ✅ works
}
```

### Local Values
![alt text](image-19.png)

### Dynamic block and splat expressions
Dynamic blocks are used to generate repeated nested blocks inside a resource, based on a variable.
```
dynamic "<block_name>" {
  for_each = <collection>

  content {
    # block configuration using each.value
  }
}
```
![alt text](image-20.png)

**Splat operator (*) and iterator**
![alt text](image-21.png)