# ghana-regions-and-towns-api
Regions and their corresponding cities in Ghana

# Description
This api allows developers to get their desired cities and regions faster and easier.

# Usage

Request-Type = POST,
Set Content-Type: application/json.
Endpoint: https://www.bgsgroups.com/projects/vSkyapi/regions/list/


1. To get all regions with their corresponding cities, send a post with they fields as
```
 body = { 
  "*": "*"
 }
 ```

2.i. To get all cities in  a specific region
```
body = {
   "Greater Accra": "*"
}
```

 2.ii. To get all cities for spcified regions
 ```
 body = {
   "Greater Accra": "*",
   "Volta": "*",
   ...
}
```

3.i. To get all data for multiple cities and their corresponding regions
```
body = {
   "*": ["ho", "keta", "funsi", "weija", ...]
}
```

3.ii. To get all data for a specific city with its corresponding region

 ``` 
 body = {
  "*": "ho"
}
```
  
If all goes well 
```
@return 
      {
       "vSky_code": "002",
       "vSky_msg": { 
                     "allregions": [array of towns]
                     }
       }
```
