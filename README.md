# DatabaseAssignment12

After spending reasonable amount of time to figure out Docker directly installed on windows (have just swithed from running Docker from VM/vagrant), it seems there is a error I simply could not overcome.

I have used CMD (commandline) to run the following statements:

    docker --version
    Docker version 18.09.2, build 6247962

    docker run -d --name neo4j --rm --publish=7474:7474 --publish=7687:7687 --env NEO4J_AUTH=neo4j/fancy!99Doorknob neo4j
    38c09ffdcbf8c8fbce9d4929d7f787fa731e87b93bc5c85ce6db94aeeab18296

    docker ps -a
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                      NAMES
    38c09ffdcbf8        neo4j               "/sbin/tini -g -- /d…"   10 seconds ago      Up 9 seconds        0.0.0.0:7474->7474/tcp,    7473/tcp, 0.0.0.0:7687->7687/tcp   neo4j
    
The container is created using Caspers startup Docker code and it is possible to enter the site http://localhost:7474/browser/ 
and use neo4j's graph database. The next statement is the problem

    docker run -it -v %cd%:/var/lib/neo4j/import bash
  
It gives me the error message:

    docker: Error response from daemon: Drive sharing failed for an unknown reason.
    See 'docker run --help'.



