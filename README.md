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
    
The container is created using Casper's startup Docker code and it is possible to enter the site http://localhost:7474/browser/ 
and use neo4j's graph database. The next statement is the problem

    docker run -it -v %cd%:/var/lib/neo4j/import bash
  
To mount/volume your hosts files into sharing apparently needs login and password:

![image](https://user-images.githubusercontent.com/40825848/56875308-5cddc600-6a40-11e9-8059-6c2858117213.png)

Even the The login credintials are inputtet, it keeps giving me the error message:

    docker: Error response from daemon: Drive sharing failed for an unknown reason.
    See 'docker run --help'.

If the mount can be done the following statement should be excecuted:

        LOAD CSV WITH HEADERS FROM "file:///some2016UKgeotweets.csv" AS row 
            FIELDTERMINATOR ";"
        return row
        LIMIT 1

But as the files are not mounted inside Docker container it gives the error:

        Neo.ClientError.Statement.ExternalResourceFailed: Couldn't load the external resource at: file:/var/lib/neo4j/import/some2016UKgeotweets.csv


The same goes for below statement

![image](https://user-images.githubusercontent.com/40825848/56877017-7b958a00-6a4b-11e9-9b29-fb854a6062ad.png)


Unfortunately exercise 2 and 3 could not be solved


