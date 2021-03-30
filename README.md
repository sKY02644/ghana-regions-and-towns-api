# Ghana-Regions-And-Cities-API
Regions and their corresponding cities in Ghana

# Description
This api allows developers to get their desired cities and regions faster and easier.

# Usage
```
Method = POST.

Content Type: application/json.

Data format: JSON

URL: https://ghanaregionsapi.herokuapp.com/{endpoint}
```


1. To get all regions with their corresponding cities, send a post with the body as
```
endpoint: 'list/'

 body = { 
  "*": "*"
 }
 ```

2.i. To get all cities in  a specific region
```
endpoint: 'list/'

body = {
   "Greater Accra": "*"
}
```

 2.ii. To get all cities for spcified regions
 ```
 endpoint: 'list/'

 body = {
   "Greater Accra": "*",
   "Volta": "*",
   ...
}
```

3.i. To get all data for multiple cities and their corresponding regions
```
endpoint: 'list/'

body = {
   "*": ["ho", "keta", "funsi", "weija", ...]
}
```

3.ii. To get all data for a specific city with its corresponding region

 ``` 
 endpoint: 'list/'

 body = {
  "*": "ho"
}
```

3.iii. To get total number of cities in all regions 
```
  endpoint: 'details/'
 
 body = {
     "/": "/",
 }
 
 @return {
     "vSky_code": "002",
     "vSky_msg": {
         "total_regions": 11,
         "total_cities": 200,
             "detailed_view": {
                     "Volta": 10,
                     "Central": 4,
                     "Western": 15
                     ...
                 }
             }
         }

```

3.iv.  To get total cities in a specific region plus region(s) with their corresponding cities and the correct order
```
endpoint: 'details/'

body = {
    "Accra": "/",
    "Cenral": ["Weija", ...],
    "Bono": ["Brekum", ...],
    ...
}

@return {
    "vSky_code": "002",
    "vSky_msg": {
        "detailed_view": {
                "Greater Accra": 10,
                ...
            },
        "checked": {
                "Central": {  "Weija"=>false, "Ho"=>false, "Apam"=>true, ... },
                "Bono": { "Brekum"=>true, "Ho"=>false, "Apam"=>false, ... },
                ...
            },
        "correct_order": {
                    "Greater Accra": ["Weija", ...],
                    "Volta": ["Ho", ...],
                    "Central": ["Apam", ...],
                    "Bono": ["Brekum", ...],
                    ...
                }
        }
    }
 
 ```
 
 Tested body against endpoint "https://ghanaregionsapi.herokuapp.com/api/regions/details/"
 
 ```
  {
     "Accra": "/",
     "Central": ["Abetifi", "Elmina"],
     "Volta": ["Ho", "Keta", "Togo", "/", "Weija"],
     "Savannah": ["Bole", "Buipe", "Damango", "Salaga", "Sawla", "Tolon"],
     "Upper West": ["Funsi", "Gwollu", "Issa", "Jirapa", "Kaleo", "Lambussie", "Lawra", "Nadowli", "Nandom", "Tumu", "Wa", "Wechiau", "Mampong"],
     "central": "/",
     "Eastern": ["Mampong", "Adukrom"],
     "Ashanti": ["Mampong", "Airport"]
  }

```
  
Results should be in this format 
```
@return 
      {
       "vSky_code": "002",
       "vSky_msg": { 
                     "allregions": [array of towns]
                     }
       }
```

# Sample codes 
   # PHP-cURL
   ```
   <?php

    $curl = curl_init();
    $body = "{\"Greater Accra\": \"*\"}";

    curl_setopt_array($curl, array(
      CURLOPT_URL => "https://ghanaregionsapi.herokuapp.com/api/regions/{endpoint},
      CURLOPT_RETURNTRANSFER => true,
      CURLOPT_ENCODING => "",
      CURLOPT_MAXREDIRS => 10,
      CURLOPT_TIMEOUT => 0,
      CURLOPT_FOLLOWLOCATION => true,
      CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
      CURLOPT_CUSTOMREQUEST => "POST",
      CURLOPT_POSTFIELDS =>$body,
      CURLOPT_HTTPHEADER => array(
        "Content-Type: application/json"
      ),
    ));

    $response = curl_exec($curl);

    curl_close($curl);
    echo $response;

    ?>
  ```
  # cURL
  ```
  curl --location --request POST 'https://ghanaregionsapi.herokuapp.com/api/regions/{endpoint}' \
--header 'Content-Type: application/json' \
--data-raw '{"Greater Accra": "*"}'
 ```
 
 # Nodejs-Native
 ```
   var https = require('follow-redirects').https;
   var fs = require('fs');

   var options = {
     'method': 'POST',
     'hostname': 'ghanaregionsapi.herokuapp.com',
     'path': '/api/regions/{endpoint}',
     'headers': {
       'Content-Type': 'application/json'
     },
     'maxRedirects': 20
   };

   var req = https.request(options, function (res) {
     var chunks = [];

     res.on("data", function (chunk) {
       chunks.push(chunk);
     });

     res.on("end", function (chunk) {
       var body = Buffer.concat(chunks);
       console.log(body.toString());
     });

     res.on("error", function (error) {
       console.error(error);
     });
   });

   var postData = JSON.stringify({"*":["Aputuogya","ho","Keta","Funsi","Gwollu","Kpetoe","Kpeve","Weija","Westhills","toogo"]});

   req.write(postData);

   req.end();
 ```
 
 # Python-Requets
 ```
 import requests

  url = "https://ghanaregionsapi.herokuapp.com/api/regions/{endpoint}"

  payload = "{\r\n   \"*\": [\"Aputuogya\", \"ho\", \"Keta\", \"Funsi\", \"Gwollu\", \"Kpetoe\", \"Kpeve\", \"Weija\", \"Westhills\", \"toogo\"]\r\n}"
  headers = {
    'Content-Type': 'application/json'
  }

  response = requests.request("POST", url, headers=headers, data = payload)

  print(response.text.encode('utf8'))

 ```

# Error codes
```
"006": "INCORRECT_PARAMETER_TYPE"

"009": "NO_DATA_FOUND"

"017": "DATA_NOT_FOUND"

"011": "EMPTY_VALUES_PASSED"

"018": "INCORRECT_REQUEST_FORMAT"

"008": "REQUEST_FILE_NOT_FOUND"

"007": "REQUEST_BODY_EMPTY"

"013": "HEADER_VALUE_ERROR"

"012": "INCORRECT_HEADERS_SENT"

"005": "REQUEST_METHOD_FAILED"

```


# Json file provided by
```
https://github.com/codingoliver/ghana-cities.git
```
