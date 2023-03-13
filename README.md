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
