## Insert or Update
```
PUT /<target>/_doc/<_id>
POST /<target>/_doc/
PUT /<target>/_create/<_id>
POST /<target>/_create/<_id>

{
    "first_name" : "Bambang",
    "last_name" : "Gunawan"
}
```
## Update Partial
```
POST /<target>/_update/<_id>
{
    "doc": {
        "first_name": "Ahmad"
    }
}
```
## Get Data
```
{
    GET /<tagrget>/_doc/<_id>
}
```
## Delete Data
```
{
    DELETE /<tagrget>/_doc/<_id>
}
```