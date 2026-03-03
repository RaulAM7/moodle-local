# Moodle local con Docker Compose

## URL local
- `http://localhost:8082`

## Credenciales
- Usuario admin: `admin`
- Password admin: `Admin1234!Admin1234!`
- Email admin: `admin@example.com`

> Si ya existía un volumen persistente (`mariadb_data`), la contraseña del admin
> puede haber cambiado en una ejecución anterior.

## Base de datos
- Motor: MariaDB
- DB: `moodle`
- Usuario: `moodle`
- Password: `moodle`
- Root password: `root`

## Arrancar
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose up -d
```

## Mantener Moodle lanzado
- No ejecutes `sudo docker compose down` justo después de `up -d`.
- Usa estos comandos para validar estado y seguir logs sin apagar:
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose ps
sudo docker compose logs -f --tail=200 moodle
```

## Parar
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose down
```

## Borrar datos persistentes (opcional, no automático)
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose down -v
```

## Ver estado y logs
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose ps
sudo docker compose logs -f --tail=200 moodle db
```

## Volúmenes persistentes
- `mariadb_data`
- `moodle_data`
- `moodledata_data`

## Nota sobre permisos Docker
Si añades el usuario al grupo `docker`, el cambio aplica tras cerrar sesión y volver a entrar.
Hasta entonces, usa `sudo docker ...`.

## Actualizar mod_edukami
1. `cd /home/reboot/Escritorio/edukamiUniverse-moodle`
2. `git pull`
3. `npm install`
4. `npm run build`
5. `cd /home/reboot/Escritorio/moodle-local`
6. `sg docker -c "docker compose up -d --force-recreate moodle"`
7. `sg docker -c "docker compose exec -T moodle php /var/www/html/admin/cli/purge_caches.php"`
8. `sg docker -c "docker compose exec -T moodle php /var/www/html/admin/cli/upgrade.php --non-interactive"`

> `npm run build` recrea la carpeta `dist/`; por eso es importante recrear el
> contenedor `moodle` para que el bind mount de `/mod/edukami` apunte al `dist`
> actualizado.
