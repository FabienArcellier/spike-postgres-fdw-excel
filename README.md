# Spike about usage of foreign datawrapper

## Getting started

* `docker-compose up` : load the docker infrastructure

## Interroger un fichier excel

```sql
CREATE EXTENSION postgres_fdw;
CREATE EXTENSION multicorn; -- middleware to code an FDW in python

CREATE SERVER excel foreign data wrapper multicorn options (
    wrapper 'fabien_fdw.ExcelForeignDataWrapper'
);

CREATE FOREIGN TABLE spatial (
    pid int,
    date timestamp,
    mission character varying,
    vol_habite boolean,
    pays character varying,
    satellite_deploye boolean,
    objective character varying
) server excel options (path '/data/spatial.xlsx', sheet 'spatial', rowid_column 'pid');

select * from spatial;
select pays, count(*) from spatial group by pays;

insert into spatial values (41, '2025-01-01', 'mission 1', true, 'France', true, 'objectif 1');
```
