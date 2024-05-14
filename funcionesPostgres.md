Redondear
```postgresql
-- Al menor o mayor
select round(14.7);

-- Con decimales
select round(14.78956, 2);

-- Borra los decimales
select trunc(14.78956);
select trunc(14.78956, 2);

-- Redondea siempre para arriba, retorna entero
select ceil(13.2)

```
Valores absolutos
```postgresql
select abs(-30)
```

Divisiones
```postgresql
-- Toma solo la parte entera
select div(30,2);

-- Residuo
select mod(4,3);
```

Raíz cúbica
```postgresql
-- Con doble precisión
select cbrt(64)
```

Potencia
```postgresql
-- Número , Potencia
select pow(2,3)
```