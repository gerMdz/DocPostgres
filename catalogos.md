* Obtener listado de base de datos
```postgresql
SELECT * from PG_DATABASE;
-- identificación de las bases
SELECT OID from PG_DATABASE;
-- + nombre
SELECT OID, DATNAME from PG_DATABASE;
-- + dba
SELECT OID, DATNAME, DATDBA from PG_DATABASE;

-- Los datos de auth
SELECT * from PG_AUTHID;
SELECT OID, ROLNAME from PG_AUTHID;

-- join tablas
SELECT D.OID, D.DATNAME, D.DATDBA, A.rolname from PG_DATABASE D
	INNER join PG_AUTHID A
	ON A.oid = D.datdba
WHERE A.rolname = 'gerardo';

-- Ver los esquemas
SELECT * FROM pg_namespace

-- Ver todos los objetos de Postgres
SELECT * FROM pg_class;

-- Ver solo tablas
SELECT * FROM pg_tables;

-- Ver indices
SELECT * FROM pg_index;

SELECT i.indexrelid, C.relname FROM pg_index I
inner join pg_class C
on C.OID = I.indexrelid;

```