Running a sample Docker container on Marathon
=============================================

Where I've used SSH tunnels to present Marathon on localhost:8080:

`curl -X POST -H "Content-Type: application/json" http://localhost:8080/v2/apps -d@docker-marathon.json`

        {
          "container": {
            "type": "DOCKER",
            "docker": {
              "image": "libmesos/ubuntu"
            }
          },
          "id": "ubuntu",
          "instances": 1,
          "cpus": 0.5,
          "mem": 512,
          "uris": [],
          "cmd": "while sleep 10; do date -u +%T; done"
        }
