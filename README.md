# Microserivicio Autenticación
Estudiante : Betty Rodriguez
## Ejecutar el Proyecto

### Requisitos Previos
- PHP 8.2 o superior
- Composer
- Node.js y npm
- MySQL 

### Instalación y Configuración

1. **Clonar el repositorio**
   ```bash
   git clone https://github.com/saoricoder/G7_microservicio_autenticacion.git
   cd G7_microservicio_autenticacion
   ```

2. **Instalar dependencias de PHP**
   ```bash
   composer install
   ```

3. **Instalar dependencias de Node.js**
   ```bash
   npm install
   ```

4. **Configurar el archivo .env**
   ```bash
   cp .env.example .env
   php artisan key:generate
   ```

5. **Configurar la base de datos**
   - Crear la base de datos `db_users` en MySQL
   - Actualizar las credenciales en el archivo `.env`:
     ```
     DB_CONNECTION=mysql
     DB_HOST=127.0.0.1
     DB_PORT=3306
     DB_DATABASE=db_users
     DB_USERNAME=root
     DB_PASSWORD=
     ```

6. **Ejecutar migraciones**
   ```bash
   php artisan migrate
   ```


### Ejecutar en Desarrollo

**Opción 1: Usar el script de desarrollo integrado**
```bash
composer run dev
```
Este comando ejecutará simultáneamente:
- Servidor de Laravel (`php artisan serve`)
- Queue listener (`php artisan queue:listen`)
- Vite dev server (`npm run dev`)

**Opción 2: Ejecutar servidores por separado**
```bash
# Terminal 1 - Servidor de Laravel
php artisan serve

# Terminal 2 - Vite dev server
npm run dev

# Terminal 3 - Queue listener (si es necesario)
php artisan queue:listen
```

### Ejecutar en Producción

1. **Configurar variables de entorno**
   ```bash
   # En .env
   APP_ENV=production
   APP_DEBUG=false
   ```

2. **Optimizar la aplicación**
   ```bash
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   npm run build
   ```



### Comandos Útiles

```bash
# Limpiar caché
php artisan config:clear
php artisan route:clear
php artisan view:clear

```

## 🚀 Rutas del Proyecto


### Rutas API - Autenticación
**Base:** `/api/auth`

#### Rutas Públicas
| Método | Ruta | Descripción |
|--------|------|-------------|
| `POST` | `/api/auth/register` | Registro de nuevos usuarios con perfil |
| `POST` | `/api/auth/login` | Inicio de sesión y generación de token |

#### Rutas Protegidas (Requieren Token)
| Método | Ruta | Descripción |
|--------|------|-------------|
| `POST` | `/api/auth/logout` | Cierre de sesión y eliminación de token |
| `GET` | `/api/auth/me` | Información completa del usuario autenticado |
| `GET` | `/api/auth/user` | Datos básicos del usuario (id, nombre, email, rol) |

### Perfiles de Usuario
El sistema implementa tres perfiles con diferentes niveles de permisos:

- **usuario**: Usuario estándar con permisos de lectura
- **administrador**: Acceso completo a todos los recursos

### Colección Postman
Para facilitar las pruebas, se incluye una colección completa de Postman en la carpeta `/postman` con:
- Todos los endpoints configurados
- Variables de entorno
- Scripts de prueba automáticos
- Documentación de uso

---

**El microservicio está listo para validar usuarios según su perfil mediante tokens de Laravel Sanctum.**

