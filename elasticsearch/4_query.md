POST /`<target>`/_search
## Match
```
{
    "query":{
      "match_all":{}
   }
}
---
{
   "query":{
      "match" : {
         "first_name": "Bambang"
      }
   }
}
```
## Range
- gte | >=
- gt  | >
- lte | <=
- lt  | <
```
{
   "query":{
      "range":{
         "age":{
            "gte":20
         }
      }
   }
}
```
## Compound (Boolean Query)
- must (and)
- filter
- should (or)
- must_not (!=)
```
{
   "query": {
      "bool" : {
         "must_not" : {
             "range": {
                 "age": {"lte" : 20}
             }
         }
      }
   }
}
---
{
   "query": {
      "bool" : {
         "must" : [
             {
                 "match": {
                     "first_name": "Fitri"
                 }
             },
             {
                 "match": {
                     "last_name": "Anggraeni"
                 }
             }
         ]
      }
   }
}
```