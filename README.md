Overview
========

The purpose of this project is to implement a ETL Pipeline using Apache Airflow.

Here is the steps in the ETL Pipeline:

1. Extract or collect weather data from a REST API endpoint.
2. Transform the retrieved data into a JSON.
3. Load the transformed data into PostgreSQL database.

This readme describes the contents of the project, as well as how to run Apache Airflow on your local machine.

Project Contents
================

Your Astro project contains the following files and folders:

- dags: This folder contains the Python files for your Airflow DAGs. By default, this directory includes one example DAG:
  - `etlweatherdag.py`: This DAG shows a simple ETL pipeline that calls a REST API endpoint to collect the weather data based on the latitude and longitude, transforms it into JSON and loads the data into a PostgreSQL database.
  - `example_astronauts`: This DAG shows a simple ETL pipeline example that queries the list of astronauts currently in space from the Open Notify API and prints a statement for each astronaut. The DAG uses the TaskFlow API to define tasks in Python, and dynamic task mapping to dynamically print a statement for each astronaut. For more on how this DAG works, see our [Getting started tutorial](https://www.astronomer.io/docs/learn/get-started-with-airflow).
- Dockerfile: This file contains a versioned Astro Runtime Docker image that provides a differentiated Airflow experience. If you want to execute other commands or overrides at runtime, specify them here.
- docker-compose.yml: This file contains a versioned PostgreSQL database image.
- include: This folder contains any additional files that you want to include as part of your project. It is empty by default.
- packages.txt: Install OS-level packages needed for your project by adding them to this file. It is empty by default.
- requirements.txt: Install Python packages needed for your project by adding them to this file. It is empty by default.
- plugins: Add custom or community plugins for your project to this file. It is empty by default.
- airflow_settings.yaml: Use this local-only file to specify Airflow Connections, Variables, and Pools instead of entering them in the Airflow UI as you develop DAGs in this project.

Technologies
============

* Python
* Astro
* Apache Airflow
* PostgreSQL

Pre-requisites
==============

* Install the Astro CLI using the [link](https://www.astronomer.io/docs/astro/cli/install-cli).

Deploy Your Project Locally
===========================

1. Start Airflow on your local machine by running 'astro dev start'.

This command will spin up 4 Docker containers on your machine, each for a different Airflow component:

- Postgres: Airflow's Metadata Database
- Webserver: The Airflow component responsible for rendering the Airflow UI
- Scheduler: The Airflow component responsible for monitoring and triggering tasks
- Triggerer: The Airflow component responsible for triggering deferred tasks

2. Verify that all 4 Docker containers were created by running 'docker ps'.

Note: Running 'astro dev start' will start your project with the Airflow Webserver exposed at port 8080 and Postgres exposed at port 5432. If you already have either of those ports allocated, you can either [stop your existing Docker containers or change the port](https://www.astronomer.io/docs/astro/cli/troubleshoot-locally#ports-are-not-available-for-my-local-airflow-webserver).

3. Access the Airflow UI for your local Airflow project. To do so, go to http://localhost:8080/ and log in with 'admin' for both your Username and Password.
4. Create the connections for PostgreSQL and the Weather API endpoint from the Airflow UI > Admin > Connections:
   * PostgreSQL
     * Connection Id: postgres_default
     * Connection Type: Postgres
     * Host: `<Get this from the Docker Containers>`
     * Login: postgres
     * Password: postgres
     * Port: 5432
   * Weather API
     * Connection Id: open_meteo_api
     * Connection Type: HTTP
5. Navigate to the DAG and run it manually to make sure that it retrieve the data by calling the API,  transforms it and loads it into PostgreSQL database.

You should also be able to access your Postgres Database at 'localhost:5432/postgres' by using any Database Client like DBeaver.

Deploy Your Project to Astronomer
=================================

If you have an Astronomer account, pushing code to a Deployment on Astronomer is simple. For deploying instructions, refer to Astronomer documentation: https://www.astronomer.io/docs/astro/deploy-code/

Contact
=======

For any inquiries or feedback, please contact me at [nikhil.komakula@outlook.com](mailto:nikhil.komakula@outlook.com).
