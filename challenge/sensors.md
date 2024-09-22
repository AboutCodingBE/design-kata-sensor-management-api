# Sensors

There are 3 different sensor models: the TS50X (temperature sensor), the PH-05 (pressure-humidity sensor) and the Trite ( temperature,
humidity and pressure).  

All 3 these sensors have firmware and a configuration in order to function correctly. An example of something that can be configured
is the endpoint to which the sensors need to send their information. Every new sensor has a base factory firmware and a base configuration 
installed. This is necessary so that the sensor can receive events that trigger either a configuration update or a firmware update.  

Sensors will get signals to start updates of either configuration or firmware. When such a signal is received, a sensor will check which
tasks have been queued. So the API needs a way for sensors to fetch the next tasks that is scheduled. Sensors will update their activity status when 
an update (which is scheduled with by a task) is either scheduled or when they are updating or when they are done. **Sensors need a way
to let the management system keep track of their status**. 

The TS50X and the PH-05 are sensors that were originally invented and created at your company. You can tell, because their firmware
is versioned like this: **v50.01.13R04**. The Trite is a different story. The rights to produce Trite sensors were bought from a
company that no longer had the capabilities of producing. The Trite was their bestselling sensor and so your company bought the rights
and thus also the market for this sensor. The firmare of the Trite is versioned by date: V202409011013.  

When customers require more information about sensors, this is an example of what they should be seeing: 

```json
{
  "serial": 123456789098789,
  "type": "TS50X",
  "status": "online",
  "current_configuration": "some_oonfiguration.cfg",
  "current_firmware": "FW:23-09-2022:03",
  "created_at": "2022-03-31 11:26:08",
  "updated_at": "2022-10-18 17:53:48",
  "status_name": "Idle",
  "next_task": null,
  "task_count": 5,
  "activity_status": 1,
  "task_queue": [211345600, 3343123345] 
}
```

An explanation of some of the fields:  
###### Status

A sensor can have the following statuses:

|Status name	|Description|
|--|-|
|Online|The sensor is online and capable of sending information|
|Disconnectd	|The sensor is not online and cannot send information|
|Error|The sensor is in an error state and cannot function normally|

###### Activity status

A sensor can have the following activity status: 

|Status name	|Status id	|Description|
|--|--|--|
|Idle	|1	|The sensor doesn’t have any tasks|
|Awaiting	|2	|A task has been scheduled, the device is waiting for execution|
|Updating	|3	|The device is doing an update|