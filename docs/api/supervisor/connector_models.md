---
title: "Connector Models"
---

These models are describing objects that will used by the connector plugin

## Remote Device

| key               | type           | description                                           |
| ----------------  | -------------- | ----------------------------------------------------- |
| id                | string         | Unique uuid for device                                |
| name              | string         | Friendly name of device                               |
| type              | string         | `usb` or `serial`                                     |
| server_address    | string         | Thr IP address of remote device server                |
| server_port       | int            | The port of the remote device server                  |
| bind_options      | string         | Device bind options for connecting                    |
| ssl_configuration | int or null    | Id of the ssl configuration used                      |
| status            | string         | `connected`, `disconnected` or `disabled`             |
| auto_connect      | bool           | `true` if device should be auto connect on restart    |

## SSL Configuration

| key              | type           | description                                           |
| ---------------- | -------------- | ----------------------------------------------------- |
| id               | int            | Id of ssl configuration                               |
| name             | string         | Friendly name for configuration                       |
| enabled          | bool           | `true` if this connection uses stunnel                |
| verifyChain      | bool           | `true` if stunnel should verify certificate           |
| caChain          | string or null | x509 CA certificate data                              |
| options          | string or null | extra ssl options                                     |

## Driver

| key              | type           | description                                           |
| ---------------- | -------------- | ----------------------------------------------------- |
| name             | string         | Name of driver to load                                |