```postgresql

-- inner join en ambas tablas
select * from nombre_tabla
inner join tabla_relacionada alias
    on alias.campo = nombre_tabla.campo_relaciondo

-- left join en tablas de la izquierda
select * from nombre_tabla
left join tabla_relacionada alias
    on alias.campo = nombre_tabla.campo_relaciondo

-- right join en tablas de la derecha
select * from nombre_tabla
right join tabla_relacionada alias
    on alias.campo = nombre_tabla.campo_relaciondo
```

```postgresql
-- union no trae columnas repetidas
select p.nombre_pro, p.precio_pro from producto p
where precio_pro < 400
   union
select p.nombre_pro, p.precio_pro from producto p
where nombre_pro like '%gr';

-- union all trae columnas repetidas
select p.nombre_pro, p.precio_pro from producto p
where precio_pro < 400
   union all
select p.nombre_pro, p.precio_pro from producto p
where nombre_pro like '%gr';

-- intersect solo aquellos registros que se repiten
select p.nombre_pro, p.precio_pro from producto p
where precio_pro < 400
   intersect
select p.nombre_pro, p.precio_pro from producto p
where nombre_pro like 'S%';
```