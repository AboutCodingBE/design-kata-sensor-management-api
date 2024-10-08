# design-kata-sensor-management-api

## READ THIS BEFORE STARTING

This is a design kata project. This means that the project is bigger and more complex than the regular easy kata exercises you
often see. Since proper software design is all about deciding how to split up problems into smaller problems, a design kata
needs to be a bit more complex.  

I still have to do this exercise, so there is no example yet. But don't let that stop you from trying yourself!  

## The problem description

Imagine that you work for a sensor manufacturer. Your company makes different types of sensors and sells these. Your job is to create 
a REST api to manage all of these sensors. Customers, that means companies who buy the sensors, need to be able to manage these sensors. 
The sensors also need to be able to fetch some information to manage themselves. Managing these sensors has different aspects:  

#### Sensors aspect

Customers need to be able to read information about sensors and update sensors that the own. **It is very important that customers do not have 
access to sensors they don’t own!**  

Sensor administrators are people who are part of the manufacturing process. Administrators need to be able to add newly produced sensors to the 
api, up to a maximum of 500 sensors. So you need to provide a way to upload information for a maximum of 500 sensors.   

There is nothing required to delete a sensor. Once a sensor has been manufactured, it’s intended to stay for a long time.

In order to start you will need more information about sensors. [Continue reading here](./challenge/sensors.md).  

#### Tasks aspect

Another aspect is tasks. If a customer wants to update the firmware or the configuration of any of these sensors, they need to schedule a task to 
do so. A task also gets a unique number. Tasks can be queued and thus a sensor can make a request to fetch the next task that is waiting. Tasks 
can be deleted/cancelled as long as they haven't been taken up by a sensor. A customer always schedules a task for one sensor. It is not possible
to schedule one task to update multiple sensors.  

A task itself can be updated. If a sensor is done with a task, the status of the task needs to be updated. Users of the API need to also be 
able to see the history of tasks for a certain sensor and wether or not that task was a success, a failure or if it was cancelled.  

As with the sensors aspect, **it is very important that customers cannot access tasks from other customers**!

In order to start you will need more information about tasks. [Continue reading here](./challenge/tasks.md).  

#### Files aspect

The last aspect is file management. When a configuration update task is created, users need to specify which configuration file needs 
to be uploaded to the sensor. Customers should be able to upload their own configuration files. In order to do so, they should be able to 
download a template to fill in with their own values. So these files need to be managed and stored somewhere. A customer needs to be able to 
look at all the configuration files owned by their company.  

A user should also be able to look at all the firmware versions for a particular type of sensor. They cannot manage any of that. New firmware 
verions should be pushed automatically into the API system.  

**File information**

Customers can ask for more information about a certain file (be it a configuration file or a firmware version file). The result
should look like this:  

```json
{
  "id": "a3e4aed2-b091-41a6-8265-2185040e2c32",
  "type": "configuration",
  "name": "enable_new_endpoint.cfg"
}
```

As with the sensors and the tasks aspect, **it is very important that customers cannot access configuration files from other customers**!

## About the challenge itself

This is quite the challenge. Just like in real life, there is a lot of information. I can imagine that this might feel overwhelming. But it 
reality, it is not all that hard.  

#### The main complexities in this challenge

There are a few aspects that make this challenge really challenging. 

- The first thing is the sheer load of information. That is something you will encounter on the job as well, at least if you want to become
 a real valuable asset. Being able to manage a huge load of information and create a solution for it, that is a big part of what we are 
 learning in this About Coding Dojo. 
- The second thing is security. Security doesn't have to be super complex. But in this challenge, it is important. Anything related to 
 customers should be only for that customer. It cannot be that one customer can get their hands on any information intended for another 
 customer. So you will need to find a way to deal with that
- Another aspect that will make this a bit more challenging is finding solutions to store and get information with security in mind. You
 are free to apply anything, but modelling will have some challenges.  

If you need more tips on how to start with this challenge, [you can find them here!](./challenge/tips/tips.md)
