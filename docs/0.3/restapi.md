# Rest API

## GET appmaster/<appId>?detail=&lt;true|false&gt;
Query information of an specific application of Id appId

Example:
```bash
curl http://127.0.0.1:8090/appmaster/2
```
Sample Response:
```
{
  "status": "active",
  "appId": 2,
  "appName": "wordCount",
  "appMasterPath": "akka.tcp://app2-executor-1@127.0.0.1:62525/user/daemon/appdaemon2/$c",
  "workerPath": "akka.tcp://master@127.0.0.1:3000/user/Worker1",
  "submissionTime": "1425925651057",
  "startTime": "1425925653433",
  "user": "foobar"
}
```


## DELETE appmaster/&lt;appId&gt;
shutdown application appId

## GET appmasters
Query information of all applications

Example:
```bash
curl http://127.0.0.1:8090/appmasters
```
Sample Response:
```
{
  "appMasters": [
    {
      "status": "active",
      "appId": 1,
      "appName": "dag",
      "appMasterPath": "akka.tcp://app1-executor-1@127.0.0.1:62498/user/daemon/appdaemon1/$c",
      "workerPath": "akka.tcp://master@127.0.0.1:3000/user/Worker1",
      "submissionTime": "1425925483482",
      "startTime": "1425925486016",
      "user": "foobar"
    }
  ]
}
```

## GET config/app/&lt;appId&gt;
Query the configuration of specific application appId

Example:
```bash
curl http://127.0.0.1:8090/config/app/1
```
Sample Response:
```
{
    "gearpump" : {
        "appmaster" : {
            "extraClasspath" : "",
            "vmargs" : "-server -Xms512M -Xmx1024M -Xss1M -XX:MaxPermSize=128m -XX:+HeapDumpOnOutOfMemoryError -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=80 -XX:+UseParNewGC -XX:NewRatio=3"
        },
        "cluster" : {
            "masters" : [
                "127.0.0.1:3000"
            ]
        },
        "executor" : {
            "extraClasspath" : "",
            "vmargs" : "-server -Xms512M -Xmx1024M -Xss1M -XX:MaxPermSize=128m -XX:+HeapDumpOnOutOfMemoryError -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=80 -XX:+UseParNewGC -XX:NewRatio=3"
        },
        "jarstore" : {
            "rootpath" : "jarstore/"
        },
        "log" : {
            "application" : {
                "dir" : "logs"
            },
            "daemon" : {
                "dir" : "logs"
            }
        },
        "metrics" : {
            "enabled" : true,
            "graphite" : {
                "host" : "127.0.0.1",
                "port" : 2003
            },
            "logfile" : {},
            "report-interval-ms" : 15000,
            "reporter" : "akka",
            "retainHistoryData" : {
                "hours" : 72,
                "intervalMs" : 3600000
            },
            "retainRecentData" : {
                "intervalMs" : 15000,
                "seconds" : 300
            },
            "sample-rate" : 10
        },
        "netty" : {
            "base-sleep-ms" : 100,
            "buffer-size" : 5242880,
            "fulsh-check-interval" : 10,
            "max-retries" : 30,
            "max-sleep-ms" : 1000,
            "message-batch-size" : 262144
        },
        "netty-dispatcher" : "akka.actor.default-dispatcher",
        "scheduling" : {
            "scheduler-class" : "org.apache.gearpump.cluster.scheduler.PriorityScheduler"
        },
        "serializers" : {
            "[B" : "",
            "[C" : "",
            "[D" : "",
            "[F" : "",
            "[I" : "",
            "[J" : "",
            "[Ljava.lang.String;" : "",
            "[S" : "",
            "[Z" : "",
            "org.apache.gearpump.Message" : "org.apache.gearpump.streaming.MessageSerializer",
            "org.apache.gearpump.streaming.task.Ack" : "org.apache.gearpump.streaming.AckSerializer",
            "org.apache.gearpump.streaming.task.AckRequest" : "org.apache.gearpump.streaming.AckRequestSerializer",
            "org.apache.gearpump.streaming.task.LatencyProbe" : "org.apache.gearpump.streaming.LatencyProbeSerializer",
            "org.apache.gearpump.streaming.task.TaskId" : "org.apache.gearpump.streaming.TaskIdSerializer",
            "scala.Tuple1" : "",
            "scala.Tuple2" : "",
            "scala.Tuple3" : "",
            "scala.Tuple4" : "",
            "scala.Tuple5" : "",
            "scala.Tuple6" : "",
            "scala.collection.immutable.$colon$colon" : "",
            "scala.collection.immutable.List" : ""
        },
        "services" : {
            # gear.conf: 112
            "host" : "127.0.0.1",
            # gear.conf: 113
            "http" : 8090,
            # gear.conf: 114
            "ws" : 8091
        },
        "task-dispatcher" : "akka.actor.pined-dispatcher",
        "worker" : {
            # reference.conf: 100
            # # How many slots each worker contains
            "slots" : 100
        }
    }
}

```

## GET master
Get information of masters

Example:
```bash
curl http://127.0.0.1:8090/master
```
Sample Response:
```
{
  "masterDescription": {
    "leader": [
      "master@127.0.0.1",
      3000
    ],
    "cluster": [
      [
        "127.0.0.1",
        3000
      ]
    ],
    "aliveFor": "642941",
    "logFile": "/Users/foobar/gearpump/logs",
    "jarStore": "jarstore/",
    "masterStatus": "synced",
    "homeDirectory": "/Users/foobar/gearpump"
  }
}
```

## GET metrics/app/&lt;appId&gt;/&lt;metrics path&gt;
Query metrics information of a specific application appId
Filter metrics with path metrics path

Example:
```bash
curl http://127.0.0.1:8090/metrics/app/3/app3.processor2
```
Sample Response:
```
{
  "appId": 3,
  "path": "app3.processor2",
  "metrics": []
}
```

## GET workers/&lt;workerId&gt;
Get information of specific worker

Example:
```bash
curl http://127.0.0.1:8090/workers/1096497833
```
Sample Response
```
{
  "workerId": 1096497833,
  "state": "active",
  "actorPath": "akka.tcp://master@127.0.0.1:3000/user/Worker0",
  "aliveFor": "77042",
  "logFile": "/Users/foobar/gearpump/logs",
  "executors": [],
  "totalSlots": 100,
  "availableSlots": 100,
  "homeDirectory": "/Users/foobar/gearpump"
}
```

The worker list can be returned by query master/ Rest service.

## GET workers
Get information of all workers.

Example:
```bash
curl http://127.0.0.1:8090/workers
```
Sample Response:
```
[
  {
    "workerId": 307839464,
    "state": "active",
    "actorPath": "akka.tcp://master@127.0.0.1:3000/user/Worker0",
    "aliveFor": "18445",
    "logFile": "/Users/foobar/gearpump/logs",
    "executors": [],
    "totalSlots": 100,
    "availableSlots": 100,
    "homeDirectory": "/Users/foobar/gearpump"
  },
  {
    "workerId": 485240986,
    "state": "active",
    "actorPath": "akka.tcp://master@127.0.0.1:3000/user/Worker1",
    "aliveFor": "18445",
    "logFile": "/Users/foobar/gearpump/logs",
    "executors": [],
    "totalSlots": 100,
    "availableSlots": 100,
    "homeDirectory": "/Users/foobar/gearpump"
  }
]
```





