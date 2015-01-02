Running a docker container via Chronos
======================================

Where I've used an SSH tunnel to present the Chronos endpoint on localhost:4400:

`curl -L -H "Content-Type: application/json" -X POST -d@docker-chronos.json http://localhost:4400/scheduler/iso8601`

        { 
         "schedule": "R\/2015-01-02T19:35:00Z\/PT2M",
         "name": "dockerjob",
         "container": {
           "type": "DOCKER",
           "image": "libmesos/ubuntu"
         },
         "cpus": "0.5",
         "mem": "512",
         "uris": [],
         "command": "while sleep 10; do date -u +%T; done"
        }
