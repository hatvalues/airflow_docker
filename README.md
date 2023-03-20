# airflow_docker
Airflow Docker Compose environment

### First steps
Download the docker-compose.yml file
`curl -LfO --url https://airflow.apache.org/docs/apache-airflow/2.5.1/docker-compose.yaml`

Create the directory structure under home
`mkdir -p ./dags ./logs ./plugins`

On Linux, configure the host user id
`echo -e "AIRFLOW_UID=$(id -u)" > .env`

Run the following to initialise the database:
`docker compose up airflow-init`

### Ready to go

`docker compose up`

Access the web interface at http://localhost:8080

### Clean stop

`docker compose down --volumes --rmi all`

### Recovering from errors (do not do this in production)

`docker compose down --volumes --remove-orphans`

Then remove the entire (working) directory.
Start again with downloading the docker-compose.yml file

### More on set up here

https://airflow.apache.org/docs/apache-airflow/stable/howto/docker-compose/index.html

## First Steps

On the docker compose environment we can access the API using localhost:8080 or $ENDPOINT_URL on Linux

(https://airflow.apache.org/docs/apache-airflow/stable/stable-rest-api-ref.html)

#### Check system status
`curl -X GET --user "airflow:airflow" "${ENDPOINT_URL}/health"`

#### Check the pools
`curl -X GET --user "airflow:airflow" "${ENDPOINT_URL}/api/v1/pools"`

#### Check the pools
`curl -X GET --user "airflow:airflow" "${ENDPOINT_URL}/api/v1/dags"`

#### Enqueue a dag run
curl -X POST --user "airflow:airflow" "${ENDPOINT_URL}/api/v1/dags/tutorial_dag/dagRuns" \
-H 'Content-Type: application/json' \
--user "airflow:airflow" \
-d '{
    "dag_run_id": "test_run",
    "logical_date": "2023-03-14T14:15:22Z",
    "conf": { }
}'

#### Docker compose commands
`docker-compose run airflow-worker airflow info`

#### CLI commands using the bash shortcut
* down load the bash shortcut
`curl -LfO 'https://airflow.apache.org/docs/apache-airflow/2.1.1/airflow.sh'`

`chmod +x airflow.sh`

* try the following commands
`./airflow.sh info`

`./airflow.sh bash`

`./airflow.sh python`

#### CLI in the bash
To view a dag definition - you can find the names using the web UI, or for self-code dags, the name is in the python definition file in the dags directory.

`airflow dags show <dag_name>`