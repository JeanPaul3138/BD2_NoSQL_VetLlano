# VetLlano - Sistema de Gestión Veterinaria (MongoDB NoSQL)

Proyecto de diseño, implementación, optimización y conexión de una base de datos orientada a documentos en **MongoDB** para la clínica veterinaria **VetLlano** (Villavicencio, Meta), desarrollado para el curso **Bases de Datos II**.

## Estructura del Proyecto

* `datos_iniciales.js`: Creación de las 4 colecciones (`propietarios`, `mascotas`, `consultas`, `servicios`), reglas de validación `$jsonSchema` e inserción de 60 documentos iniciales.
* `consultas.js`: 10 consultas de negocio, 4 operaciones de actualización, 3 pipelines de agregación (`$lookup`, `$unwind`, `$group`) y 3 índices con análisis de rendimiento (`explain`).
* `crud_vetllano.py`: Script en Python (`pymongo`) que ejecuta las operaciones CRUD sobre la colección `servicios` leyendo credenciales desde variables de entorno.
* `.env.example`: Plantilla de variables de entorno para la conexión segura.
* `respaldo/`: Archivos JSON exportados con el respaldo completo de las colecciones.

## Requisitos Previos

* **MongoDB Community Server 7.0+** (con autenticación habilitada en `mongod.cfg`).
* **MongoDB Shell (`mongosh`)** y **MongoDB Compass**.
* **Python 3.10+** con `pip`.

## Instalación y Ejecución

### 1. Clonar el repositorio e instalar dependencias
```bash
git clone [https://github.com/JeanPaul3138/BD2_NoSQL_VetLlano.git](https://github.com/JeanPaul3138/BD2_NoSQL_VetLlano.git)
cd BD2_NoSQL_VetLlano
py -m pip install pymongo python-dotenv
```

### 2. Configurar variables de entorno
Crea un archivo `.env` en la raíz del proyecto basado en `.env.example`:
```env
MONGO_URI=mongodb://app_vetllano:TU_PASSWORD@localhost:27017/vetllano_db
DB_NAME=vetllano_db
```

### 3. Cargar estructura, validaciones y datos iniciales
Ejecuta el script inicial con el usuario administrador de la base de datos:
```bash
mongosh "mongodb://admin_vetllano:TU_PASSWORD_ADMIN@localhost:27017/vetllano_db?authSource=admin" datos_iniciales.js
```

### 4. Ejecutar consultas, agregaciones e índices
Corre el script de operaciones y verificación de rendimiento (`COLLSCAN` vs `IXSCAN`):
```bash
mongosh "mongodb://app_vetllano:TU_PASSWORD@localhost:27017/vetllano_db" consultas.js
```

### 5. Ejecutar el CRUD desde Python
```bash
py crud_vetllano.py
```

### 6. Restauración de respaldo
Desde **MongoDB Compass**, conéctate a `vetllano_db`, selecciona cada colección y utiliza **Add Data > Import JSON or CSV file** cargando los archivos ubicados en la carpeta `respaldo/`.
