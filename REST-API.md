![AiLight](images/ailight_logo.png)

_Since release: **v0.5.0**_

The **AiLight** firmware has a powerful [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) interface, which acts as a simple web service. Use it as your tool for those situations where you don't have/want to use [MQTT](https://en.wikipedia.org/wiki/MQTT). This REST API will help you to use your light as you like it, by integrating it into apps, websites or something else.

# Requests
The **AiLight** REST API accepts requests over HTTP at

`http://<your_ailight_ip_address_or_hostname_here>/api`.

All POST requests must use a [JSON](https://en.wikipedia.org/wiki/JSON) body with the Content-Type header set to `'application/json'`.

*NOTE: Be aware that TSL/SSL is currently not supported, meaning all traffic is transmitted unencrypted, including your API Key!*

## Authentication
The **AiLight** REST API requires an API Key in order to access it. Your API Key can be found/defined in the settings page of the Web UI. Keep in mind that this key has full control of your light, so please keep it private.

To authenticate for the API, use your API Key in the header of your request in the following manner:

`'API-Key: <your_api_key_here>'`

You can make a request from any app, though how you do that may depend on if you are writing a script or using a programming language. If you have a terminal and the [cURL](https://curl.haxx.se/) utility, you can perform requests from the command line. In this Wiki, all examples are demonstrated with the curl utility.

### Example: About Details

***Request***

`curl -X GET http://<your_ailight_ip_address_or_hostname_here>/api/about -H 'API-Key: <your_api_key_here>'`

***Response***

```JSON
{
  "app_name": "AiLight",
  "app_version": "0.5.0",
  "build_date": "Jul 31 2017",
  "build_time": "15:02:58",
  "memory": 1048576,
  "free_heap": 29032,
  "cpu_frequency": 80,
  "manufacturer": "Ai-Thinker",
  "model": "RGBW Light",
  "device_ip": "192.168.5.204",
  "mac": "4D:06:D4:1C:48:54"
}
```

## Responses
Responses are always returned in JSON format, except for responses related to the HTTP status codes 404 and 405: these do not contain an HTTP body. Keys are either present with a non-empty value, or entirely absent from the response. Empty values are: null, false, "", [], and {}.

## HTTP Status Codes
- `200 OK`: Everything worked as expected.
- `400 Bad Request`: Usually this results from missing a required parameter or header.
- `401 Unauthorized`: No valid API Key provided.    
- //`403 Forbidden`: The API Key is not valid for that Request
- `404 Not Found`: The requested item doesn't exist
- `405 Method Not Allowed`: The requested HTTP method is not available for the requested item

## Errors
Error responses (any non-200 error code) may contain information on the kind of error that happened. The response JSON may have the following fields:

- `error`: A machine-readable code, same as the HTTP status code (e.g. 400, 401, etc.)
- `message`: A human-readable error message.

**Example Error Response**:
```JSON
{
    "error": "400",
    "message": "The required API Key is missing"
}
```

# API Endpoints

## GET /api/light
Gets the current state of this light, similar as is shown on the 'Light' page in the Web UI.

### Response

| Field         | Type      | Values       | Description
|---------------|-----------|--------------|---------------------------------------------------|
| `state`       | Integer   | "ON"/"OFF"   | The current state of the light                    |
| `brightness`  | Integer   | 0-255        | The brightness level of the light                 |
| `white_value` | Integer   | 0-255        | The level of the White LED's of the light         |
| `color_temp`  | Integer   | 0-500        | The color temperature of the ligh (in Mired)      |
| `color`       | Object    | -            | An object with the below RGB values               |
| `color.r`     | Integer   | 0-255        | The red color level of the light                  |
| `color.g`     | Integer   | 0-255        | The green color level of the light                |
| `color.b`     | Integer   | 0-255        | The blue color level of the light                 |
| `gamma`       | Boolean   | true/false   | Whether Gamma Correction is enabled of the light  |


### Example

***Request***

`curl -X GET http://<your_ailight_ip_address_or_hostname_here>/api/light -H 'API-Key: <your_api_key_here>'`

***Response***

```JSON
{
  "state": "ON",
  "brightness": 65,
  "white_value": 10,
  "color_temp": 370,
  "color": {
      "r": 128,
      "g": 0,
      "b": 56
   },
  "gamma": false
}
```

## PATCH /api/light
Update your light parameters (e.g. color, brightness, etc.)

## GET /api/about
Gets general information about this light and the **AiLight** firmware, similar as is shown on the 'About' page in the Web UI.

### Response

| Field           | Type    | Description
|-----------------|---------|--------------------------------------------------|
| `app_name`      | String  | The name of this **AiLight** firmware            |
| `app_version`   | String  | Version of the installed **AiLight** firmware    |
| `build_date`    | String  | Date the **AiLight** firmware was built/compiled |
| `build_time`    | String  | Time the **AiLight** firmware was built/compiled |
| `memory`        | Integer | Memory capacity (in bytes)                       |
| `free_heap`     | Integer | Available free memory (in bytes)                 |
| `cpu_frequency` | Integer | CPU Speed (in MHz)                               |
| `manufacturer`  | String  | The name of the manufacturer of this light       |
| `model`         | String  | The name of this lights' model                   |
| `device_ip`     | String  | The assigned IP address of this light            |
| `mac`           | String  | The assigned MAC address of this light           |

### Example

***Request***

`curl -X GET http://<your_ailight_ip_address_or_hostname_here>/api/about -H 'API-Key: <your_api_key_here>'`

***Response***

```JSON
{
  "app_name": "AiLight",
  "app_version": "0.5.0",
  "build_date": "Jul 31 2017",
  "build_time": "15:02:58",
  "memory": 1048576,
  "free_heap": 29032,
  "cpu_frequency": 80,
  "manufacturer": "Ai-Thinker",
  "model": "RGBW Light",
  "device_ip": "192.168.5.204",
  "mac": "4D:06:D4:1C:48:54"
}
```
