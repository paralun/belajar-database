## Create Index
```
PUT /product
{
  "settings": {
    "index": {
      "number_of_shards": 3,
      "number_of_replicas": 1
    }
  }
}
```
### Request Body
- aliases
- mappings
- settings

## Delete Index
```
DELETE /<index>
DELETE /product
```
## Get Index
```
GET /<target>
GET /product
```