Creo función

```postgresql
create function saludo()
    returns character varying
as
$$
begin
    return 'Cadena especial';
end

$$
    language plpgsql;

-- Llamo a la función
select saludo()
```

Borrar funciones
```postgresql
drop function nombre_funcion
```

Funciones con operaciones

```postgresql
create or replace function fn_descuento(precio integer)
    returns integer
as
$$
declare
    descuento numeric(18, 2);
begin
    descuento = precio * 0.1;
    return descuento;
end

$$
    language plpgsql;

-- Aplicando funciones a una consulta
select producto.nombre_pro, producto.precio_pro precio, fn_descuento(precio_pro)
from producto
```

Reutilizando funciones

```postgresql
create or replace function fn_a_pagar(precio integer)
    returns numeric
as
$$
declare
    descuento numeric(18, 2);
    a_pagar   numeric(18, 2);
begin
    descuento = fn_descuento(precio);
    a_pagar = precio - descuento;
    return a_pagar;
end

$$
    language plpgsql;

-- Usando la función
select producto.nombre_pro, producto.precio_pro precio, fn_descuento(precio_pro), fn_a_pagar(precio_pro)
from producto
```

Multiples variables

```postgresql
create or replace function fn_descuento_percent(precio integer, percent integer)
    returns numeric
as
$$
declare
    descuento numeric(18, 2);
    a_pagar   numeric(18, 2);
begin
    descuento = precio * percent / 100.0;
    a_pagar = precio - descuento;
    return descuento;
end

$$
    language plpgsql;

-- Llamando a la función

select producto.nombre_pro,
       producto.precio_pro precio,
       fn_descuento_percent(precio_pro, 30),
       fn_a_pagar(precio_pro)
from producto
```

Funciones con condicionales

```postgresql
create or replace function fn_mensaje_pedido(total integer)
    returns character varying
as
$$
declare
    mensaje character varying;
begin
    if total < 501 then
        mensaje = 'Descuento menor';
    else
        mensaje = 'Mayor descuento';
    end if;

    return mensaje;
end

$$
    language plpgsql;

-- Usando la función
select producto.nombre_pro,
       producto.precio_pro precio,
       fn_mensaje_pedido(precio_pro)
from producto
```

```postgresql
-- Obtener diferencia entre fechas en formato humano
select age(current_date, '1969-08-21');

-- Obtener diferencia entre fechas en formato humano, pero diferenciando una parte
select date_part('year', age(current_date, '1969-08-21'));
```

```postgresql
-- Función para el cálculo
create or replace function fn_get_age_message(fecha_nac timestamp)
    returns character varying
as
$$
declare
    years integer;
    mensaje character varying;
begin

    years = date_part('year', age(current_date, fecha_nac));
    if years < 18 then
        mensaje = 'Menor de edad';
    else
        mensaje = 'Mayor de edad';
    end if;

    return mensaje;
end

$$
    language plpgsql;

-- Usando la función
select cliente.nombre_cliente,
       cliente.fecha_nacimiento,
       fn_get_age_message(cliente.fecha_nacimiento)
from cliente;
```

```postgresql
-- Listando tablas
create or replace function fn_get_products()
    returns setof producto
as
$$
declare
begin

    return query select  * from producto;
end

$$
    language plpgsql;

-- Usando la función
select * from fn_get_products();
```

```postgresql
-- Funciones de listado con algo dificultad
create or replace function fn_get_products_range_precio(precio_1 integer, precio_2 integer)
    returns setof producto
as
$$
declare
begin

    return query select  * from producto where  precio_pro between precio_1 and precio_2;
end

$$
    language plpgsql;

-- Usando la sección
select * from fn_get_products_range_precio(200, 500);
select nombre_pro from fn_get_products_range_precio(200, 500);
```

```postgresql
-- Función listar tablas con parámetros
create or replace function fn_get_products_by_id(id_producto integer)
    returns setof producto
as
$$
declare
begin

    return query select  * from producto where  id = id_producto;
end

$$
    language plpgsql;

-- Usando la función
select * from fn_get_products_by_id(1);
```

```postgresql
create or replace function listaCliente()
returns table(id int, nombre_cliente varchar)
as
    $$
    select id, nombre_cliente
    from cliente
    $$
language sql;

-- Usando la función
select * from listacliente();

-- Agregando parámetros
create or replace function nombre_funcion(v_id int)
returns table(id int, nombre_cliente varchar)
as
    $$
    select id, nombre_cliente
    from cliente
    where id=v_id
    $$
language sql;
-- Usando la función
select * from nombre_funcion(2);

-- Con join
create or replace function fn_cliente_pedido()
returns table(id int, nombre_cliente varchar, id_pedido int)
as
    $$
    select c.id, c.nombre_cliente, p.id_pedido
    from cliente c
        join public.pedido p on c.id = p.codigo_cliente
    $$
language sql;
-- Usando la función
select * from fn_cliente_pedido();
```

Voids
```postgresql
-- Create
create or replace function insertClient(v_nombre varchar, v_address varchar, v_fecha_nacimiento timestamp)
    returns void
as
$$
    insert into cliente(nombre_cliente, direccion_cliente, fecha_nacimiento)
    values (v_nombre, v_address, v_fecha_nacimiento)
$$

language sql;
-- Usando la función
select insertClient('Clau', 'Isla 1 puesto 2', '2000-05-06');

-- Update
create or replace function updateClient(v_id int, v_nombre varchar, v_address varchar, v_fecha_nacimiento timestamp)
    returns void
as
$$
update cliente
set nombre_cliente    = v_nombre,
    direccion_cliente = v_address,
    fecha_nacimiento  = v_fecha_nacimiento
where id = v_id
$$
    language sql;
-- Usando la función
select updateClient(3, 'Claudia', 'Isla 1 puesto 2', '2000-05-06');
```

