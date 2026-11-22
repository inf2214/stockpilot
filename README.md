# StockPilot

**Sistema de gestión de inventario con alertas inteligentes para PyMEs de retail.**

## 📖 Descripción del Problema

Pequeños y medianos comercios gestionan su inventario de forma manual o con sistemas aislados, lo que provoca **quiebres de stock** (pérdida de ventas) y **sobreinventario** (capital inmovilizado). La falta de datos centralizados impide un reabastecimiento eficiente y la toma de decisiones basada en información.

## 💡 Nuestra Solución

StockPilot es una aplicación web full-stack que centraliza el control de inventario, automatiza la detección de productos en riesgo de agotarse y proporciona visibilidad en tiempo real sobre el estado del almacén, permitiendo a los negocios **recuperar el control y reducir pérdidas**.

## ✨ Características Principales (Fase 1 - MVP)

-   **Autenticación con Roles:** Acceso seguro para administradores y vendedores.
-   **Catálogo de Productos:** Gestión completa (CRUD) con SKU, precios y umbral de stock mínimo.
-   **Gestión de Proveedores:** Registro de contactos para el reabastecimiento.
-   **Movimientos de Stock:** Registro de entradas y salidas con historial de auditoría.
-   **Motor de Alertas:** Notificaciones visuales de productos con stock bajo o agotado.
-   **Dashboard con Métricas:** Visualización de productos críticos, valor del inventario y ventas recientes.

## 🛠️ Stack Tecnológico

-   **Backend:** Python 3.12, Django 5, Django REST Framework
-   **Base de Datos:** PostgreSQL 16
-   **Frontend:** React 18, TypeScript, Vite, Tailwind CSS
-   **Contenedores:** Docker, Docker Compose
-   **CI/CD:** GitHub Actions
-   **Despliegue:** Render (Backend), Vercel (Frontend)

## 🚀 Estado del Proyecto

🏗️ **En desarrollo activo** - Actualmente construyendo la Fase 1 (MVP).

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo `LICENSE` para más detalles. (Añadiremos este archivo más adelante).

## 🗄️ Modelo de Datos
erDiagram
    USER ||--o{ STOCK_MOVEMENT : "registra"
    CATEGORY ||--o{ PRODUCT : "clasifica"
    SUPPLIER ||--o{ PRODUCT : "suministra"
    PRODUCT ||--o{ STOCK_MOVEMENT : "tiene"

    USER {
        uuid id PK
        string email UK
        string password
        string first_name
        string last_name
        enum role "ADMIN | SELLER"
        boolean is_active
        datetime date_joined
    }

    CATEGORY {
        int id PK
        string name UK
        text description
        datetime created_at
    }

    SUPPLIER {
        int id PK
        string name
        string contact_name
        string email
        string phone
        text address
        boolean is_active
        datetime created_at
        datetime updated_at
    }

    PRODUCT {
        int id PK
        string sku UK
        string name
        text description
        int category_id FK
        int supplier_id FK
        decimal cost_price
        decimal sale_price
        int stock_current
        int stock_minimum
        boolean is_active
        datetime created_at
        datetime updated_at
    }

    STOCK_MOVEMENT {
        bigint id PK
        int product_id FK
        uuid user_id FK
        enum movement_type "ENTRY | EXIT"
        int quantity
        decimal unit_price
        string reference
        text notes
        datetime created_at
    }
