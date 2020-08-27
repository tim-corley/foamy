# Overview & Setup

- jenkins is a tool for process automation
- intuitive web interface
- free & open source
- access to many plugins

[DOCS](https://www.jenkins.io/doc/book/)

## install via Docker

see: [docker install notes](../docker/overview.md)

```bash
➜  ~ sudo docker pull jenkins/jenkins:lts
➜  ~ sudo docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
jenkins/jenkins     lts                 697d76eba014        9 days ago          677MB
hello-world         latest              bf756fb1ae65        7 months ago        13.3kB
➜  ~ sudo docker run --detach --publish 8080:8080 --volume jenkins_home:/var/jenkins_home --name jenkins jenkins/jenkins:lts
➜  ~ sudo docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

in browser, go to: `localhost:8080` and login (w/ password provided via last command) / install plugins
