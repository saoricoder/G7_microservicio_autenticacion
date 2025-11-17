
## Ejecutar el Proyecto

### Requisitos Previos
- PHP 8.2 o superior
- Composer
- Node.js y npm
- MySQL 

### Instalación y Configuración

1. **Clonar el repositorio**
   ```bash
   git clone [URL_DEL_REPOSITORIO]
   cd pry_microservicio_autenticacion
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
     DB_USERNAME=tu_usuario
     DB_PASSWORD=tu_contraseña
     ```

6. **Ejecutar migraciones**
   ```bash
   php artisan migrate
   ```

7. **Compilar assets (opcional para producción)**
   ```bash
   npm run build
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

3. **Configurar el servidor web** (Apache/Nginx) apuntando a la carpeta `public`

### Comandos Útiles

```bash
# Limpiar caché
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Ejecutar tests
composer run test
# o
php artisan test

# Ver logs
php artisan log:tail

# Reiniciar queue
php artisan queue:restart
```

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework. You can also check out [Laravel Learn](https://laravel.com/learn), where you will be guided through building a modern Laravel application.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains thousands of video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the [Laravel Partners program](https://partners.laravel.com).

### Premium Partners

- **[Vehikl](https://vehikl.com)**
- **[Tighten Co.](https://tighten.co)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel)**
- **[DevSquad](https://devsquad.com/hire-laravel-developers)**
- **[Redberry](https://redberry.international/laravel-development)**
- **[Active Logic](https://activelogic.com)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

## Functional Routes

This authentication microservice provides the following functional routes:

### Web Routes
- `GET /` - Welcome page
- `GET /react` - React application page

### API Routes (Authentication)
Base prefix: `/api/auth`

#### Public Routes
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login

#### Protected Routes (Require Authentication)
- `POST /api/auth/logout` - User logout
- `GET /api/auth/me` - Get authenticated user information with role
- `GET /api/auth/user` - Get authenticated user details (id, name, email, role)

All protected routes require authentication via Laravel Sanctum token.
