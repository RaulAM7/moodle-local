# Moodle local con Docker Compose

## URL local
- `http://localhost:8080`

## Credenciales
- Usuario admin: `admin`
- Password admin: `admin`
- Email admin: `admin@example.com`

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
sudo docker compose logs -f --tail=200 moodle mariadb
```

## Volúmenes persistentes
- `mariadb_data`
- `moodle_data`
- `moodledata_data`

## Nota sobre permisos Docker
Si añades el usuario al grupo `docker`, el cambio aplica tras cerrar sesión y volver a entrar.
Hasta entonces, usa `sudo docker ...`.
