# Docker Voting App

This is the Docker demo voting app that has 3 services:
* Result - A Node.js webapp which shows the results of the voting in real time
* Vote - A front-end web app in Python which lets you vote between two options
* Worker - A Java worker which consumes votes and stores them in Postgres

![Architecture diagram](architecture.png)

The voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.

## Result service configuration
| Name                    | Required | Type        | Default Value  | Description                                       |
|-------------------------|----------|-------------|----------------|---------------------------------------------------|
| DB_HOST                 | Yes      | ENV         | postgres       | Postgres database hostname                        |
| DB_PASSWORD             | Yes      | ENV         | changeme       | Postgres database password                        |
| DB_USER                 | Yes      | ENV         | user           | Postgres database username                        |
| SQL_USER                | Yes      | ENV or File | sqladmin       | The username for the SQL Server database.         |

Simple build:
``` 
cd result/
docker build -f Dockerfile -t voting-app/result:1.0 .
```

## Vote service configuration
| Name                    | Required | Type        | Default Value  | Description                                       |
|-------------------------|----------|-------------|----------------|---------------------------------------------------|
| REDIS_HOST              | Yes      | ENV         | redis          | Redis database hostname                           |
| REDIS_PASSWORD          | Yes      | ENV         |                | Redis database password                           |

Simple build:
``` 
cd vote/
docker build -f Dockerfile -t voting-app/vote:1.0 .
```

## Worker service configuration
| Name                    | Required | Type        | Default Value  | Description                                       |
|-------------------------|----------|-------------|----------------|---------------------------------------------------|
| DB_HOST                 | Yes      | ENV         |                | Postgres database hostname                        |
| DB_PASSWORD             | Yes      | ENV         |                | Postgres database password                        |
| DB_USER                 | Yes      | ENV         |                | Postgres database username                        |
| REDIS_HOST              | Yes      | ENV         |                | Redis database hostname                           |
| REDIS_PASSWORD          | Yes      | ENV         |                | Redis database password                           |

Simple build:
``` 
cd worker/
docker build -f Dockerfile -t voting-app/worker:1.0 .
```