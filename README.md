# Postgres version managment scripts 
These scripts used for veriosn managmnet op a postgres DB

## prerequisite
1. python (https://www.python.org/downloads/)
2. expect (Debian: apt-get update && apt-get install -y expect; Mac: sudo port install expect;)
3. psql (apt-get update && apt-get install -y postgresql-client)
4. pyrseas (https://pyrseas.readthedocs.io/en/latest/install.html)
5. pip install psycopg2
6. pip3 install psycopg_c
7. pip3 install psycopg_binary
8. pip3 install libpq

## env variables (scrips will read .env file from [../.env](../.env))
1. DB_HOST: DB server hostname/ip 
2. DB_PORT: DB server port
3. DB_USER: User with access to DB
4. DB_PASSWORD: User password
5. DB_DATABASE: Database name to export to yaml

## [Link to Pyrseas docs](https://pyrseas.readthedocs.io/_/downloads/en/latest/pdf/)
* The following scripts is used for:
1. Create a yaml snapshot of a db and store it [here](../snapshot/CMS-DB.yaml)
2. Create a diff between the [snapshot](../snapshot/DB.yaml) and a destenation DB using the snapshot form 1. and saving it [here](../snapshot/DB-DIFF.sql)
3. Create & update a destenation DB (this step runs step 2. and 3. in one script)

## 1. [pg-dbtoyaml.sh](./pg-dbtoyaml.sh)

Bash script used to create a snapshot from your DEV DB (snpashot will be used to update the production DB)

run: 
```bash pg-dbtoyaml.sh```

Links to docks: 
1. https://pyrseas.readthedocs.io/en/latest/dbtoyaml.html

---

## 2. [pg-yamltodb.sh](./pg-yamltodb.sh)

Bash script used to create a diff between snapshot created in section 1 and destenation DB

run: 
```bash pg-yamltodb.sh```

Links to docks: 
1. https://pyrseas.readthedocs.io/en/latest/yamltodb.html

---

## 3. [pg-update.sh](./pg-update.sh)

Bash script to create diff by calling section 2 and applying the diff created to the destenation DB (used by docker)

run: 
```bash pg-update.sh```