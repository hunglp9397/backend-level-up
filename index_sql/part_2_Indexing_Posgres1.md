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

### 2.1 Explain
```roomsql
    EXPLAIN SELECT * FROM ENGINEER;
```
![6.png](/img_guide/6.png)

+ cost: Số lượng tính toán cần để hoàn thành, Hiểu đơn giản là 0 đến 2117
+ rows: Số lượng rows mà Postgess nghĩ rằng cần scan để thực hiện query
+ width: Độ rộng trung bình của mỗi row khi thực hiện query (đơn vị byte)


### 2.2 Explain analyze:
- Explain chỉ đưa ra thông số áng chừng về chi phí. Để có con số cụ thể về executime, cần chạy lệnh sau:

```roomsql
    BEGIN;
    EXPLAIN ANALYZE SELECT *  FROM engineer;
    ROLLBACK;
```
- Ta có các thông số:
- ![7.png](/img_guide/7.png)
   + cost : số lượng tính toán cần để hoàn thành, Hiểu đơn giản là 0 đến 2117
   + loops : số lượng vòng lặp
   + planning time : thời gian lên kế hoạch cho query 
   + execution time : actual_time (thời gian cho nhiệm vụ seq scan table)  + Thời gian fetch data để hiển thị