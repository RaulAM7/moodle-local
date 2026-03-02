# Moodle local con Docker Compose

Entorno local de Moodle con `Docker Compose`, MariaDB y credenciales preconfiguradas para pruebas.

## Requisitos
- Docker instalado
- Plugin de Docker Compose (`docker compose`)
- Puerto `8080` libre en la máquina local

## Servicios incluidos
- `db`: MariaDB `10.11`
- `moodle`: imagen `moodlehq/moodle-php-apache:8.4`

## Configuración principal
- URL local: `http://localhost:8080`
- Base de datos:
  - Motor: `mariadb`
  - Host: `db`
  - Nombre DB: `moodle`
  - Usuario DB: `moodle`
  - Password DB: `moodle`
  - Root password DB: `root`

## Persistencia de datos
Se usan estos volúmenes Docker:
- `mariadb_data`
- `moodle_data`
- `moodledata_data`

Para reiniciar totalmente el entorno (eliminando datos persistentes):
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose down -v
```

## Notas de uso
- En el primer arranque, Moodle puede tardar un poco en quedar disponible.
- Si añades tu usuario al grupo `docker`, necesitas cerrar y abrir sesión para aplicar permisos; hasta entonces usa `sudo`.
- Puedes revisar estado y logs con:
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose ps
sudo docker compose logs -f --tail=200 moodle mariadb
```

## Login
- URL: http://localhost:8080
- Usuario: admin
- Password: Admin1234!Admin1234!
- Email: admin@example.com

## Comandos de uso
```bash
cd /home/reboot/Escritorio/moodle-local
sudo docker compose up -d
sudo docker compose down
sudo docker compose logs -f --tail=200 moodle
```
