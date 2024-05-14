Muestra donde se encuentra el archivo de configuración
```bash
show config_file
```

Desde la consola
```bash
# Restore psql
psql -U usuario_con_permisos Database_restore < /ruta/al/backkup/nombre_archivo.sql 

# Restore pg_restore 
pg_restore -U usuario_con_permisos -d Database_restore -v /ruta/al/backkup/nombre_archivo.dump (*.tar)
pg_restore -U usuario_con_permisos -d Database_restore --table=table_restore -v /ruta/al/backkup/nombre_archivo.dump (*.tar)
pg_restore -U usuario_con_permisos -d Database_restore --schema-only -v /ruta/al/backkup/nombre_archivo.dump (*.tar)
```
