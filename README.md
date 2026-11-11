# Unified Business Workspace - Backend

## 📖 Descripción del Módulo

Este repositorio contiene la Capa de Servidor, Lógica de Negocio y Persistencia (Backend) de la plataforma **Unified Business Workspace**.

Desarrollado en **Node.js** con el framework **Express.js**, este módulo actúa como el motor central del sistema. Se encarga de exponer la API REST, gestionar la autenticación segura (OAuth 2.0 / JWT), aplicar el Control de Acceso Basado en Roles (RBAC) y mantener la persistencia de datos corporativos. Además, soporta conexiones bidireccionales de baja latencia mediante WebSockets para las funcionalidades colaborativas.

### Tecnologías Core Integradas:
* **Node.js & Express.js**: Enrutamiento ágil y controladores de la API REST.
* **Socket.io**: Servidor de tiempo real para chat por hilos, actualización de tableros Kanban y sincronización de pizarras.
* **Prisma ORM & MySQL**: Modelado de datos seguro, tipado estático e integridad referencial estricta.

---

## ⚙️ Prerrequisitos de Software

Para levantar el servidor y la base de datos en tu máquina local, requieres:
* [Node.js](https://nodejs.org/) (Versión LTS recomendada).
* [MySQL](https://www.mysql.com/) (Servidor de base de datos relacional operativo).
* [Git](https://git-scm.com/) (Control de versiones).

---

## 🚀 Comandos de Arranque (Entorno Local)

Sigue estos pasos para poner en marcha el servidor de desarrollo y conectar la base de datos:

**1. Clonar el repositorio:**
```bash
git clone https://github.com/tu-usuario/workspace-backend.git
cd workspace-backend
```

**2. Instalar las dependencias del proyecto:**
```bash
npm install
```

**3. Configurar las variables de entorno:**
Crea el archivo local `.env` copiando la plantilla base. Es **crítico** que configures correctamente la cadena de conexión a tu base de datos MySQL local y tu firma secreta para los tokens JWT.
```bash
cp .env.example .env
```

*Ejemplo de configuración en `.env`:*
```env
PORT=3000
DATABASE_URL="mysql://usuario:contraseña@localhost:3306/workspace_db"
JWT_SECRET="tu_clave_secreta_jwt"
```

**4. Sincronizar la base de datos (Prisma):**
Una vez configurado el `.env`, sincroniza el esquema relacional con tu servidor MySQL local:
```bash
npx prisma db push
```

**5. Levantar el servidor de desarrollo:**
```bash
npm run dev
```

El servidor iniciará (generalmente en `http://localhost:3000`), activando tanto los endpoints REST (`/api/v1/...`) como el listener de Socket.io.