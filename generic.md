# Generic Device Messages


## StopDeviceCmd

**Description:** Client request to have the server stop a device from whatever actions it may be taking. This message should be supported by all devices, and the server should know how to stop any device it supports.

**Fields:**

-   *Id* (unsigned int): Message Id
-   *DeviceIndex* (unsigned int): Index of device to stop.

**Expected Response:**

-   Ok message with matching Id on successful request.
-   Error message on value or message error.

**Flow Diagram:**

![img](stopdevice_diagram.svg)

**Serialization Example:**

```json
[
  {
    "StopDeviceCmd": {
      "Id": 1,
      "DeviceIndex": 0
    }
  }
]
```


## StopAllDevices

**Description:** Sent by the client to tell the server to stop all devices. Can be used for emergency situations, on client shutdown for cleanup, etc&#x2026; While this is considered a Device Message, since it pertains to all currently connected devices, it does not specify a device index (and does not end with 'Cmd').

**Fields:**

-   *Id* (unsigned int): Message Id

**Expected Response:**

-   Ok message with matching Id on successful request.
-   Error message on value or message error.

**Flow Diagram:**

![img](stopalldevices_diagram.svg)

**Serialization Example:**

```json
[
  {
    "StopAllDevices": {
      "Id": 1
    }
  }
]
```


## SingleMotorVibrateCmd


## RawCmd
