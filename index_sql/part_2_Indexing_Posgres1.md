# Hướng dẫn Indexing 

## 1. Environment:
- Start PostgreSQL và pgAdmin4:
```shell
cd docker-config
docker-compose up -d
```
- Access to PgAdmin:
    + URL: http://localhost:5050
    + Username: pgadmin4@pgadmin.org (as a default)
    + Password: admin (as a default)
- Add a new server in PgAdmin:
    + Host name/address postgres
    + Port 5432
    + Username as POSTGRES_USER, by default: postgres
    + Password as POSTGRES_PASSWORD, by default changeme