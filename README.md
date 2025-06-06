# Servidor con Nginx Proxy, DuckDNS y Let's Encrypt

Este proyecto utiliza Docker Compose para levantar un servidor web con las siguientes funcionalidades:

- DNS dinámico con [DuckDNS](https://www.duckdns.org/)
- Servidor reverse proxy con [nginx-proxy](https://github.com/nginx-proxy/nginx-proxy)
- Certificados SSL automáticos de [Let's Encrypt](https://letsencrypt.org/) usando [acme-companion](https://github.com/nginx-proxy/acme-companion)
- Servidor web estático con Nginx

## Estructura de servicios

### 1. DuckDNS
Actualiza tu IP pública en DuckDNS automáticamente para usarla con tu subdominio personalizado.

### 2. nginx-proxy
Crea dinámicamente proxies para los servicios Docker basándose en las variables de entorno `VIRTUAL_HOST`.

### 3. acme-companion
Genera y renueva certificados SSL con Let's Encrypt automáticamente.

### 4. Web
Contenedor con Nginx que sirve archivos estáticos desde el directorio `./templates`.

## Requisitos previos

- Docker y Docker Compose instalados
- Cuenta en [DuckDNS](https://www.duckdns.org/)
- Subdominio registrado en DuckDNS
- Archivos HTML en la carpeta `./templates`

## Variables a configurar

Debes modificar los siguientes campos antes de iniciar el stack:

En `docker-compose.yml`:

```yaml
# En el servicio duckdns:
- SUBDOMAINS=tu-subdominio
- TOKEN=tu-token-de-duckdns

# En el servicio web:
- VIRTUAL_HOST=www.tu-dominio.duckdns.org,tu-dominio.duckdns.org
- LETSENCRYPT_HOST=www.tu-dominio.duckdns.org,tu-dominio.duckdns.org
