# 📮 Colección Postman - Microservicio de Autenticación

Esta carpeta contiene los archivos de configuración de Postman para probar el microservicio de autenticación con Laravel Sanctum.

## 📁 Archivos Incluidos

### 1. `UsersAuth.postman_collection.json`
Colección completa con todos los endpoints del microservicio:
- **01. Registro de Usuario** - Crea un nuevo usuario y obtiene token
- **02. Login de Usuario** - Autenticación y obtención de token
- **03. Información del Usuario (Me)** - Datos completos del usuario autenticado
- **04. Datos Básicos del Usuario** - Información básica del usuario (para otros microservicios)
- **05. Logout** - Cierre de sesión e invalidación del token

### 2. `UsersAuth.postman_environment.json`
Variables de entorno configurables:
- `base_url`: URL del servidor (por defecto: http://localhost:8000)
- `name`: Nombre del usuario para registro
- `email`: Email del usuario
- `password`: Contraseña (mínimo 8 caracteres)
- `role`: Rol del usuario (`paciente`, `doctor`, `administrador`)
- `token`: Token de autenticación (se actualiza automáticamente)
- `user_id`: ID del usuario (se actualiza después del registro)
- `user_role`: Rol actual del usuario

## 🚀 Cómo Usar

### Importar en Postman

1. **Abrir Postman**
2. **Importar la colección**:
   - Click en "Import" → "Upload Files"
   - Seleccionar `UsersAuth.postman_collection.json`
3. **Importar el entorno**:
   - Click en "Import" → "Upload Files"
   - Seleccionar `UsersAuth.postman_environment.json`

### Configurar el Entorno

1. **Seleccionar el entorno**:
   - En el dropdown de entornos (top-right), seleccionar "Microservicio Autenticación - Entorno"
2. **Modificar valores si es necesario**:
   - Click en el icono de "eye" junto al entorno
   - Click en "Edit" para cambiar valores
   - Los valores se guardan automáticamente

### Ejecutar las Pruebas

#### Flujo Recomendado:

1. **Registro** (Register):
   - Modifica el email si es necesario
   - Ejecuta el request
   - El token se guarda automáticamente

2. **Login** (si ya tienes usuario):
   - Asegúrate de tener el email correcto
   - Ejecuta el request
   - El token se actualiza automáticamente

3. **Consultar Información** (Me / User):
   - Requiere token válido (se obtiene automáticamente)
   - Ejecuta para ver datos del usuario

4. **Logout**:
   - Cierra sesión e invalida el token
   - El token se limpia del entorno

## 📋 Características de los Tests

### Scripts Automáticos
- ✅ **Validación de respuestas HTTP** (status codes)
- ✅ **Verificación de estructura JSON**
- ✅ **Guardado automático de tokens**
- ✅ **Actualización de variables de entorno**
- ✅ **Logs informativos en consola**

### Validaciones Incluidas
- **Registro**: Verifica token, usuario, rol y tipo Bearer
- **Login**: Confirma mensaje y estructura de respuesta
- **Me/User**: Valida datos completos del usuario
- **Logout**: Confirma cierre de sesión exitoso

## 🔧 Roles Disponibles

Según el controlador de autenticación:
- `paciente` - Usuario estándar (lectura)
- `doctor` - Profesional médico (lectura/escritura)
- `administrador` - Administrador del sistema (todos los permisos)

## ⚠️ Notas Importantes

1. **Token Automático**: Los tokens se guardan y actualizan automáticamente después de registro/login
2. **Logout**: Al ejecutar logout, el token se elimina del entorno
3. **Validaciones**: Los tests verifican que las respuestas tengan la estructura correcta
4. **Consola**: Revisa la consola de Postman para ver logs detallados

## 🐛 Solución de Problemas

### Error 401 (Unauthorized)
- Asegúrate de ejecutar Login primero
- Verifica que el token no haya expirado
- Revisa que el entorno esté seleccionado

### Error 422 (Validation Error)
- Verifica que el email sea único (cambia si es necesario)
- Asegúrate de que la contraseña tenga mínimo 8 caracteres
- Confirma que el rol sea uno de los valores permitidos

### Error de Conexión
- Verifica que el servidor Laravel esté ejecutándose
- Confirma que la URL base sea correcta
- Revisa que el puerto (8000) esté disponible

## 📚 Documentación Adicional

Para más información sobre el microservicio, revisa:
- [README principal](../README.md)
- Rutas API en `routes/api.php`
- Controlador en `app/Http/Controllers/Api/AuthController.php`

---

**✨ Lista para usar con Postman v9.0+**