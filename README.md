# Papeleria-HTML
# Sistema de Gestión de Inventarios — Papelería El Punto

Proyecto de aula para la asignatura **Desarrollo de Software 1**, Tecnología en Desarrollo de Software — Fundación Universitaria Tecnológico Comfenalco (Cartagena).

Migración del prototipo original en Java (Swing + archivos planos) hacia una **aplicación web** desarrollada por el equipo como programadores junior, con el objetivo de digitalizar el control de inventario y ventas de la Papelería El Punto, que actualmente se lleva de forma manual en cuadernos.

---

## 👥 Integrantes

| Código | Nombre |
|---|---|
|  | Luis Eduardo Cantillo Torres |
|  | Elías David Castilla |
|  | Geiser Eduardo Gómez Avila |
|  | Yamil Eduardo Barrio |

**Docente:** Antonio De la Valle

---

## 🎯 Objetivo del proyecto

Desarrollar una aplicación web que permita automatizar el control de inventario y el registro de ventas de la Papelería El Punto, reemplazando el registro manual en cuadernos, garantizando que la información quede centralizada en una base de datos y que cada usuario acceda solo a las funciones que le corresponden según su rol.

---

## 🛠️ Stack tecnológico

| Capa | Tecnología |
|---|---|
| Estructura | HTML5 |
| Estilos | CSS3 |
| Lógica de servidor | PHP |
| Base de datos | MySQL |
| Servidor local | XAMPP (Apache + MySQL + PHP) |
| Control de versiones | Git + GitHub |

> No se usa JavaScript en esta primera versión: toda la lógica (validaciones, cálculos, consultas) se resuelve en el servidor con PHP y se recarga la página. Esto simplifica el proyecto para un equipo que está empezando.

---

## 🔑 Roles del sistema

El sistema tiene **tres roles**, cada uno con su propia interfaz y sus propios permisos:

### 1. Cliente
- Se registra y crea su perfil.
- Consulta el catálogo de productos disponibles.
- Realiza compras (retiro en tienda o domicilio).

### 2. Vendedor
- Registra ventas en mostrador (busca producto por código, calcula total y cambio).
- Consulta el inventario disponible.
- Genera e imprime la factura de cada venta.

### 3. Administrador
- Gestiona el inventario (crear, editar, desactivar productos).
- Crea y administra perfiles de usuario (clientes, vendedores).
- Consulta reportes: balance financiero, ventas realizadas, productos más vendidos, stock bajo.
- Registra pagos a empleados.
- **No** realiza ventas — su función es de control y administración.

El acceso a cada módulo se valida en cada página PHP verificando el rol guardado en la sesión del usuario (`$_SESSION['rol']`).

---

## 🗄️ Base de datos

Motor: **MySQL**, administrado localmente con **phpMyAdmin** (incluido en XAMPP).

### Tablas principales

| Tabla | Descripción |
|---|---|
| `usuarios` | Almacena a clientes, vendedores y administradores, con su rol |
| `productos` | Inventario: código, nombre, categoría, precio de venta, precio de costo, stock, stock mínimo |
| `ventas` | Cabecera de cada venta: fecha, vendedor, cliente, tipo (mostrador/domicilio), total, efectivo recibido |
| `detalle_ventas` | Líneas de cada venta (qué productos y cuántas unidades se vendieron) |
| `pagos_empleados` | Registro de pagos realizados a los vendedores |

> El script de creación de la base de datos (`database.sql`) y el diagrama entidad-relación se encuentran en la carpeta `/docs`.

---

## 📁 Estructura del proyecto

```
papeleria-el-punto/
│
├── index.php                 # Redirige al login
├── login.php                 # Autenticación de usuarios
├── logout.php                # Cierre de sesión
│
├── /admin/                   # Módulo del Administrador
│   ├── dashboard.php
│   ├── productos.php
│   ├── usuarios.php
│   ├── reportes.php
│   └── pagos.php
│
├── /vendedor/                # Módulo del Vendedor
│   ├── ventas.php
│   ├── inventario.php
│   └── factura.php
│
├── /cliente/                 # Módulo del Cliente
│   ├── catalogo.php
│   ├── carrito.php
│   └── mis_compras.php
│
├── /includes/                # Código PHP reutilizable
│   ├── conexion.php           # Conexión a la base de datos (mysqli/PDO)
│   ├── funciones.php          # Funciones comunes (cálculos, validaciones)
│   └── auth.php               # Verificación de sesión y rol
│
├── /assets/
│   ├── /css/                  # Hojas de estilo
│   └── /img/                  # Imágenes y logo
│
├── /docs/                     # Documentación del proyecto
│   ├── database.sql
│   ├── diagrama_ER.png
│   ├── anexos/                # Contextualización, Problematización, Historias de usuario, Wireframes
│   └── Informe_Metodologico.docx
│
└── README.md
```

---

## ▶️ Cómo levantar el proyecto localmente

1. Instalar **XAMPP** (incluye Apache, MySQL y PHP).
2. Copiar la carpeta del proyecto dentro de `htdocs` (por ejemplo: `C:\xampp\htdocs\papeleria-el-punto`).
3. Iniciar los servicios **Apache** y **MySQL** desde el panel de control de XAMPP.
4. Abrir `phpMyAdmin` en `http://localhost/phpmyadmin`, crear una base de datos (por ejemplo `papeleria_el_punto`) e importar el archivo `docs/database.sql`.
5. Abrir `includes/conexion.php` y verificar que los datos de conexión (host, usuario, contraseña, nombre de la base de datos) coincidan con la configuración local.
6. Acceder al proyecto desde el navegador: `http://localhost/papeleria-el-punto`.

---

## 📖 Documentación

Como equipo de programadores junior, cada módulo del proyecto se documenta explicando:
- **Qué hace** cada archivo/página.
- **Por qué** se tomó esa decisión de diseño.
- **Cómo** se conecta con la base de datos.

Esta documentación se irá agregando como comentarios dentro del código PHP y también como archivos explicativos dentro de `/docs`, junto con los anexos académicos (Contextualización, Problematización, Historias de Usuario, Diagrama ER, Wireframes) actualizados al nuevo stack.

---

## 🗺️ Estado actual del proyecto

- [x] Definición de historias de usuario y requerimientos funcionales
- [x] Diagrama entidad-relación y modelo relacional
- [x] Definición del stack (HTML/CSS/PHP/MySQL, sin JavaScript)
- [ ] Creación de la base de datos en MySQL
- [ ] Módulo de login y sesiones por rol
- [ ] Módulo de inventario (Administrador)
- [ ] Módulo de ventas (Vendedor)
- [ ] Módulo de catálogo y compras (Cliente)
- [ ] Módulo de reportes y balance financiero
- [ ] Módulo de pagos a empleados
