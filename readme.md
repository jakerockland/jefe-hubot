jefe HuBot
===========

Idea: Setup HuBot inside a Docker container and run it on AWS. Automatically build and deploy it with CirclCI.

[![Circle CI](https://circleci.com/gh/pgarbe/jefe-hubot.svg?style=svg)](https://circleci.com/gh/pgarbe/jefe-hubot)
[![Travis CI](https://travis-ci.org/pgarbe/jefe-hubot.svg?branch=master)](https://travis-ci.org/pgarbe/jefe-hubot)


### Deploy manual to AWS ECS
1. Setup new EC2 Container Instance as described [here](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_GetStarted.html)
2. Register task definition
      aws ecs register-task-definition --cli-input-json file://$HOME/../hubot-aws-task.json
3. Start task instances
      aws ecs run-task --cluster default --task-definition hubot:X --count 1



### How to build and run it
    docker build -t jefe .
    docker run -e HUBOT_SLACK_TOKEN=xxx -d jefe

### Add new scripts
1. Add the following line in the dockerfile to install the NodeJS module:

    RUN npm install [MyHuBotModule] --save && npm install

2. Extend the external-scripts.json file with the name of the NodeJS module:

  [ "...",
    "MyHuBotModule"
    ]


### Next steps
* Persistent brain (Redis?)
* Rights & Roles
