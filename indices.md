* Los índices consumen memoria.
* Los índices se crean a una columna.

```postgresql
-- Ver los índices
select *
from PG_INDEXES;

-- Crear un índice
create index indice_nombre_cliente on cliente (nombre_cliente);

-- Crear un índice unique
create unique index unique_nombre_indice on nombre_tabla (nombre_compo);

-- Índices calculados
create index indice_calculado on detalle_pedido ((precio_venta * cantidad_prod));

-- Índices parciales
create index indice_parcial on nombre_tabla(nombre_compo) where nombre_compo = 1;    

-- Borrar un índice
drop index nombre_indice;
```

* Particionado por comando
  * Los campos de la tabla hija se reflejan en la tabla padre y al revés
```postgresql
-- Crea tabla particionada
create table personas
( id serial, nombre varchar(150), iidsexo int,
    primary key (id, iidsexo)
) partition by range (iidsexo);

-- Crea partición
create table personas_hombre partition of personas for values from (1) to (2);
create table personas_mujer partition of personas for values from (2) to (3);
```
* Herencia
  * Los campos de la tabla hija se reflejan en la tabla padre _pero no al revés_
```postgresql
-- Creo tabla inicial
create table islas
(
    id       serial,
    nombre   varchar(10),
    cantidad int
);

-- Tabla hija
create table islas_staff (check ( cantidad > 1 and cantidad < 4)) inherits (islas);

-- insert en tabla hija, se verá en tabla padre
insert into islas_staff(nombre, cantidad) values ('Isla 3', 3);
-- insert en tabla padre, no se vera en tabla hija
insert into islas(nombre, cantidad) values ('Isla 1', 4);


```