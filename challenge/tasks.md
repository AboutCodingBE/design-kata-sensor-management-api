# Tasks

Customers can use the API to create tasks for sensors. When a task is created, its status is ‘pending’ until the sensor
picks it up and performs the task. There are 2 different tasks. There are firmware update tasks and there are configuration
update tasks. Tasks can be cancelled / deleted. They are not really deleted, it is just that their status is updated to 'cancelled'. 

An update task has the following information:

```json
{
  "id": 16624171,
  "sensor_serial": 12345678909789,
  "type": "update_configuration",
  "status_id": 2,
  "attempt_count": 3,
  "created_at": "2022-10-17 16:00:07",
  "updated_at": "2022-10-17 16:49:39",
  "file_id": "a3e4aed2-b091-41a6-8265-2185040e2c32",
  "status_name": "Completed"
}
```

The file id either references an actual configuration file (which your company manages per customer) or it references a
firmware version (the actual installation file is then managed internally).  

**Type**

A task can have the following types:

| Type                 | 	Description                        |
|----------------------|-------------------------------------|
| update_firmware      | 	A task to update the firmware      |
| update_configuration | 	A task to update the configuration |

**Status**

A task can have the following statuses:

| Status name	 | Status id	 | Description                                                                  |
|--------------|------------|------------------------------------------------------------------------------|
| Pending	     | 1	         | The task is waiting to start                                                 |
| Completed	   | 2	         | The task has successfully completed                                          |
| Error	       | 3	         | The task was either interrupted by an error or it completed causing an error |
| Ongoing	     | 4	         | The task is ongoing                                                          |
| Cancelled	   | 5	         | The task was cancelled                                                       |


###### Creating tasks:

When customers want to schedule a tasks or create a task (same thing), they need to provide the following information:

```json
{
  "sensor_serial": 234545767890987,
  "file_id": "a3e4aed2-b091-41a6-8265-2185040e2c32",
  "type": "update_configuration"
}
```



