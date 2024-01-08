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

- Tạo table:
```roomsql
CREATE TABLE IF NOT EXISTS country
(
    id bigserial NOT NULL,
    country_name character varying(255),
    created timestamp without time zone,
    PRIMARY KEY (id)
);

CREATE TABLE IF NOT EXISTS engineer
(
    id bigserial NOT NULL,
    first_name character varying(255),
    last_name character varying(255),
    gender smallint NOT NULL,
    country_id bigint,
    title character varying(255),
    created timestamp without time zone,
    PRIMARY KEY (id)
);

```

- Insert 100K record tại đây:
  https://drive.google.com/file/d/1UB5g_lexnkIPrd4us_S57CaA0_yTezur/view

- Kết quả:
  ![5.png](/img_guide/5.png)
## 2. Explain Query