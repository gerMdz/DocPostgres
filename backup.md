Muestra donde se encuentra el archivo de configuración
```bash
show config_file
```

Desde la consola
```bash
# Dump común
pg_dump -U user_con_permisos nombre_database > /ruta/al/backkup/nombre_archivo.sql
# Dump con dump
pg_dump -U user_con_permisos -Fc nombre_database > /ruta/al/backkup/nombre_archivo.dump
# Dump tar
pg_dump -U user_con_permisos -Ft nombre_database > /ruta/al/backkup/nombre_archivo.tar
# Dump tabla
pg_dump -U user_con_permisos -t nombre_tabla nombre_database > /ruta/al/backkup/nombre_archivo.sql
# Dump tabla con filtro
pg_dump -U user_con_permisos -t nombre_tabla_* nombre_database > /ruta/al/backkup/nombre_archivo_*.sql
# Dump tabla con filtro y exclusión
pg_dump -U user_con_permisos -t nombre_tabla_* -T tabla_exluida nombre_database > /ruta/al/backkup/nombre_archivo_sin_excluido.sql

# Dump solo data
pg_dump -U user_con_permisos -a --data-only nombre_database > /ruta/al/backkup/nombre_archivo_data.sql

# Dump schema
pg_dump -U user_con_permisos --schema=nombre_schema nombre_database > /ruta/al/backkup/nombre_archivo_schema.sql

# Dump db
pg_dump -U user_con_permisos nombre_database > /ruta/al/backkup/nombre_archivo_database.sql

# Dump db con exclusión
pg_dump -U user_con_permisos --exclude-schema=schema_excluido nombre_database > /ruta/al/backkup/nombre_archivo_database_sin_excluido_schema.sql

# Dump db solo schema
pg_dump -U user_con_permisos --schema-only=nombre_schema nombre_database > /ruta/al/backkup/nombre_schema_only.sql

# Dump db filtro owner
pg_dump -U user_con_permisos --no-owner=nombre_owner nombre_database > /ruta/al/backkup/archivo_salida.sql

# Todas las bases
pg_dumpall -U user_con_permisos -f /ruta/al/backkup/archivo_salida.sql
pg_dumpall -U user_con_permisos -a > /ruta/al/backkup/archivo_salida.sql

# Dump globales
pg_dumpall -U user_con_permisos -g > /ruta/al/backkup/archivo_salida.sql

# Dump roles
pg_dumpall -U user_con_permisos -r > /ruta/al/backkup/archivo_salida.sql

# Dump schems
pg_dumpall -U user_con_permisos -s > /ruta/al/backkup/archivo_salida.sql

```
