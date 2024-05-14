Bloques anónimos

```postgresql
do
$$

    declare
--     defino variables
        v_number_1 int;
        v_number_2 int;
        v_result   int;
    begin
        v_number_1 := 4;
        v_number_2 := 7;
        v_result := v_number_1 + v_number_2;
        raise notice 'Resultado= %', v_result;

    end;

$$
```
Estructura if else
```postgresql
do
$$

    declare
--     defino variables
        v_name    varchar;
        v_address varchar;

        -- Inicio programa
    begin
        select nombre_cliente, direccion_cliente
        into v_name, v_address
        from cliente
        where id = 2;

--         Muestro resultado
        raise notice 'El cliente % vive en %', v_name,v_address;

    end;

$$
```

```postgresql
do
$$

    declare
--     defino variables
        v_registro record;


    begin
        --     La sentencia select en este caso tiene que estar en la misma línea que el into
        select into v_registro *
        from cliente
        where id = 2;
        raise notice
            'El cliente % y vive en % y nacio el %', v_registro.nombre_cliente, v_registro.direccion_cliente, v_registro.fecha_nacimiento;

    end;

$$
```

```postgresql
do
$$

    declare
--     defino variables
        v_registro record;


    begin
        --     La sentencia select en este caso tiene que estar en la misma línea que el into
        select into v_registro *
        from cliente
        where id = 2;
        raise notice
            'El cliente % y vive en % y nacio el %', v_registro.nombre_cliente, v_registro.direccion_cliente, v_registro.fecha_nacimiento;

    end;

$$
```

La diferencia entre rowtype y record radica en que el primero trar una fila de una tabla mientras que record trae los
datos de una consulta

Case when
```postgresql
do
$$

    declare
--     defino variables
        v_precio_venta int;
        v_precio_final int;


    begin
        --     La sentencia select en este caso tiene que estar en la misma línea que el into
        select precio_pro
        into v_precio_venta
        from producto
        where id = 4;
        case
            when v_precio_venta between 0 and 300 then v_precio_final := v_precio_venta - 0.05 * v_precio_venta;
            when v_precio_venta between 301 and 900 then v_precio_final := v_precio_venta - 0.07 * v_precio_venta;

            else v_precio_final := v_precio_venta - 0.10 * v_precio_venta;
            end case;

        raise notice 'El precio % merece un descuento y quedará en %', v_precio_venta, v_precio_final;

    end;

$$
```

Bucle
```postgresql
do
$$

    declare
        v_i int;

    begin
        -- Inicializador
        v_i := 1;

        loop
            raise notice '%', v_i;
            v_i := v_i + 1;
            exit when v_i > 10;
        end loop;

    end;
$$
```

if else anidados
```postgresql
do
$$

    declare
--     defino variables
        v_precio_venta int;
        v_precio_final int;


    begin
        --     La sentencia select en este caso tiene que estar en la misma línea que el into
        select precio_pro
        into v_precio_venta
        from producto
        where id = 4;

        if v_precio_venta between 0 and 300 then
            v_precio_final := v_precio_venta - 0.05 * v_precio_venta;
        elseif v_precio_venta between 301 and 900 then
            v_precio_final := v_precio_venta - 0.07 * v_precio_venta;
        else
            v_precio_final := v_precio_venta - 0.10 * v_precio_venta;
        end if;
        raise notice 'El precio % merece un descuento y quedará en %', v_precio_venta, v_precio_final;

    end;

$$
```

Bucle while

```postgresql
do
$$

    declare
        v_i int;

    begin
        -- Inicializador
        v_i := 1;

        while v_i < 11 loop
            raise notice '%', v_i;
            v_i := v_i + 1;
        end loop;

    end;
$$
```

Bucle for sobre una tabla
```postgresql
do
$$

    declare

ITEM record;
    begin

        for ITEM in select * from producto loop
            raise notice 'El producto %', ITEM.nombre_pro;
            end loop;


    end;
$$
```

### Bucles con select a tablas
```postgresql
do
$$
    declare

        ITEM record;
    begin

        for ITEM in select * from pedido
            loop
--                 raise notice 'Valor compra %', ITEM.total_compra;
                if ITEM.total_compra < 500 then
                    UPDATE pedido
                        set total_compra = total_compra * 0.9
                    where id_pedido = ITEM.id_pedido;
                    else
                    UPDATE pedido
                        set total_compra = total_compra * 0.85
                    where id_pedido = ITEM.id_pedido;
                end if;
            end loop;
    end;
$$
```

Cursores
```postgresql
do
$$
    declare

        cursor_pedido cursor for select *
                                 from pedido;
        row_pedido record;
    begin

        open cursor_pedido;

        fetch cursor_pedido into row_pedido;

        while FOUND
            loop
                if row_pedido.total_compra > 500 then
                    UPDATE pedido
                    set total_compra = total_compra * 1.1
                    where id_pedido = row_pedido.id_pedido;
                else
                    UPDATE pedido
                    set total_compra = total_compra * 1.2
                    where id_pedido = row_pedido.id_pedido;
                end if;
                fetch cursor_pedido into row_pedido;

            end loop;
        close cursor_pedido;

    end;
$$
```