# 🎸 GuitarLA - Tienda de Guitarras y Cursos

![GuitarLA Screenshot](./src/assets/screenshot.png)

GuitarLA es una aplicación web desarrollada con **Vue 3 + Vite** que simula una tienda online de guitarras eléctricas.  
Incluye una página principal con un modelo destacado, una sección con el catálogo completo de guitarras y un sistema básico para agregar productos al carrito de compras.

---

## 🚀 Tecnologías Utilizadas

- ⚡ **Vite** – Entorno de desarrollo rápido y optimizado.  
- 🧩 **Vue 3 (Composition API + `<script setup>`)** – Framework frontend moderno y reactivo.  
- 🎨 **CSS / SCSS / Tailwind (opcional)** – Para el diseño visual responsivo y moderno.  
- 🛒 **Vuex / Pinia (opcional)** – Para la gestión del estado global del carrito.

---

## 📸 Vista Previa

### 🟠 Modelo Destacado
Una sección superior donde se muestra el modelo **Lukather**, con su precio y botón de compra destacado.

### 🖤 Nuestra Colección
Listado de guitarras con nombre, descripción, imagen, precio y botón de **“Agregar al Carrito”**.  
Cada tarjeta está cuidadosamente diseñada para mantener consistencia visual y un estilo profesional.

---

## 🧱 Estructura del Proyecto

guitarla-vue/
├── public/
│ └── guitarras/ # Imágenes de las guitarras
├── src/
│ ├── assets/ # Recursos gráficos
│ ├── components/ # Componentes Vue
│ ├── pages/ # Vistas principales
│ ├── App.vue # Componente raíz
│ └── main.js # Punto de entrada del proyecto
├── package.json
└── vite.config.js
