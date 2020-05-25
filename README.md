# ghana-regions-and-towns-api
Regions and their corresponding cities in Ghana

# Description
This api allows developers to get their desired cities and regions faster and easier.

# Usage
```
Method = POST.

Content Type: application/json.

Data format: JSON

Endpoint: https://bgsgroupghana.com/projects/vSkyapi/regions/list/
```

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

# Sample codes 
   # PHP-cURL
   ```
   <?php

    $curl = curl_init();
    $body = "{\"Greater Accra\": \"*\"}";

    curl_setopt_array($curl, array(
      CURLOPT_URL => "https://bgsgroupghana.com/projects/vSkyapi/regions/list/",
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
  curl --location --request POST 'https://bgsgroupghana.com/projects/vSkyapi/regions/list/' \
--header 'Content-Type: application/json' \
--data-raw '{"Greater Accra": "*"}'
 ```
 
 # Nodejs-Native
 ```
   var https = require('follow-redirects').https;
   var fs = require('fs');

   var options = {
     'method': 'POST',
     'hostname': 'bgsgroupghana.com',
     'path': '/projects/vSkyapi/regions/list/',
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

  url = "https://bgsgroupghana.com/projects/vSkyapi/regions/list/"

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


# Thanks to for the json file
```
https://github.com/codingoliver/ghana-cities.git
```
