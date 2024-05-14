```bash
-- Todos los usuarios de la base

\du 
```

CREATEDB > Crea base de datos
CREATEROLE > Crea roles (usuarios)

```bash
create user name_user whit password 'new_password';
create user name_user_crea_base whit password 'new_password' createdb;
create user name_user_crea_role whit password 'new_password' createrole;
create user name_user_multi whit password 'new_password' createdb createrole;
```

Dar permisos a una tabla y campos

```bash
grant all on nombre_table to user_permiso; 
grant select on nombre_table to user_permiso;
grant accion_permitida, accion_permitida on nombre_table to user_permiso;
grant all on sequence nombre_secuencia to user_permiso;
grant select(nombre_campo) on nombre_tabla to user_permiso;
```

Revocar permisos
```postgresql
revoke all on nombre_tabla from user_permiso;
```
