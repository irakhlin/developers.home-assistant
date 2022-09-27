---
title: "Connector Endpoints"
---
import ApiEndpoint from '@site/static/js/api_endpoint.jsx'

For API endpoints marked with :lock: you need use an authorization header with a `Bearer` token.

The token is available for add-ons and Home Assistant using the
`SUPERVISOR_TOKEN` environment variable.

To see more details about each endpoint, click on it to expand it.

### SSL Configuration

<ApiEndpoint path="/connector/ssl_configurations" method="get">
Return overview information about all ssl configuration structs.

**Payload:**

| key                | type | description                                        |
| ------------------ | ---- | -------------------------------------------------- |
| ssl-configurations | list | A list of [SSL Configuration models](api/supervisor/connector_models.md#ssl-configuration)           |

**Example response:**

```json
{
  "ssl-configuration": [
    {
      "id": 1,
      "name": "Self Signed CA",
      "enabled": true,
      "verifyChain": true,
      "caChain": "-----BEGIN RSA PRIVATE KEY-----\njlQvt9WdR..",
      "options": "NO_SSLv2,NO_SSLv3,NO_TLSv1,NO_TLSv1.1"
    }
  ]
}
```
</ApiEndpoint>

<ApiEndpoint path="/connector/ssl_configurations" method="post">
Create an SSL Configuration struct for device ssl tunnels

**Payload:**

| key         | type   | optional | description                   |
| ----------- | ------ | -------- | ----------------------------  |
| name        | string | False    | The SSL Configuration name    |
| enabled     | bool   | False    | The name of the profile       |
| verifyChain | bool   | True     | The name of the profile       |
| caChain     | string | True     | The name of the profile       |
| options     | string | True     | The name of the profile       |

**Example response:**
```json
{
    "id": "1"
}
```

</ApiEndpoint>

<ApiEndpoint path="/connector/ssl_configurations/<ssl configration id>" method="get">
Get an SSL Configuration struct by Id

**Example response:**
```json
{
    "id": 1,
    "name": "Self Signed CA",
    "enabled": true,
    "verifyChain": true,
    "caChain": "-----BEGIN RSA PRIVATE KEY-----\njlQvt9WdR..",
    "options": "NO_SSLv2,NO_SSLv3,NO_TLSv1,NO_TLSv1.1"
}
```

</ApiEndpoint>

<ApiEndpoint path="/connector/ssl_configurations/<ssl configration id>" method="delete">
Delete an SSL Configuration struct by Id

</ApiEndpoint>

### Devices

<ApiEndpoint path="/connector/devices" method="get">
Return overview information about all configured devices.

**Payload:**

| key            | type | description                                        |
| -------------- | ---- | -------------------------------------------------- |
| remote-devices | list | A list of [Remote Devices models](api/supervisor/connector_models.md#remote-devices)           |

**Example response:**

```json
{
  "remote-device": [
    {
      "id": "bf09401e-850e-4302-983e-81ca2c1b00ac",
      "name": "Kitchen Bluetooth",
      "type": "usb",
      "server_address": "10.0.0.5",
      "server_port": "3240",
      "bind_options": "1-1.4",
      "ssl_configuration": 1,
      "status": "disconnected",
      "auto_connect": false,
    }
  ]
}
```

</ApiEndpoint>

<ApiEndpoint path="/connector/devices/<remote device id>" method="post">
Create a remote device

**Payload:**

| key                     | type           | description                                           |
| ----------------------- | -------------- | ----------------------------------------------------- |
| name                    | string         | Friendly name of device                               |
| type                    | string         | `usb` or `serial`                                     |
| server_address          | string         | Thr IP address of remote device server                |
| server_port             | int            | The port of the remote device server                  |
| bind_options            | string         | The installed version of the add-on                   |
| ssl_configuration       | int or null    | Id of the ssl configuration used                      |
| auto_connect            | bool           | `true` if device should be auto connect on restart    |

**Example response:**
```json
{
    "id": "bf09401e-850e-4302-983e-81ca2c1b00ac"
}
```
</ApiEndpoint>

<ApiEndpoint path="/connector/devices/<remote device id>" method="get">
Return the current status and configuration of a remote device

**Example response:**
```json
{
    "id": "bf09401e-850e-4302-983e-81ca2c1b00ac",
    "name": "Kitchen Bluetooth",
    "type": "usb",
    "server_address": "10.0.0.5",
    "server_port": "3240",
    "bind_options": "1-1.4",
    "ssl_configuration": 1,
    "status": "connected",
    "auto_connect": false,
}
```

</ApiEndpoint>

<ApiEndpoint path="/connector/devices/<remote device id>" method="delete">
Delete a configured remote device
</ApiEndpoint>

<ApiEndpoint path="/connector/devices/<remote device id>/connect" method="post">
Initiate connect/bind for remote device
</ApiEndpoint>

<ApiEndpoint path="/connector/devices/<remote device id>/disconnect" method="post">
Initiate disconnect/unbind for remote device
</ApiEndpoint>

### Drivers

<ApiEndpoint path="/connector/drivers" method="get">
Get list of loaded kernel drivers for remote devices

**Payload:**

| key          | type | description                                        |
| ------------ | ---- | -------------------------------------------------- |
| drivers      | list | A list of [Drivers models](api/supervisor/connector_models.md#drivers)           |

**Example response:**

```json
{
  "drivers": [
    {
      "name": "vhci-hcd",
    }
  ]
}
```

</ApiEndpoint>

<ApiEndpoint path="/connector/drivers" method="post">
Load a kernel driver

**Payload:**

| key                     | type           | description                                           |
| ----------------------- | -------------- | ----------------------------------------------------- |
| name                    | string         | Driver name to load                                   |

</ApiEndpoint>

<ApiEndpoint path="/connector/drivers/<driver name>" method="delete">
Unload a kernel driver
</ApiEndpoint>