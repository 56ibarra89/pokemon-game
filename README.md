# 🎮 Pokémon Guessing Game / Juego de Adivinar Pokémon

<div align="center">
  <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="PokeAPI Logo" height="100">
</div>

*Read this README in [English](#english) or [Español](#español).*

---

## 🇺🇸 English <a name="english"></a>

### 📖 About the Project
A fun and interactive "Who's that Pokémon?" guessing game built with cutting-edge web technologies. This project demonstrates the modern composition API approach in Vue 3 using TypeScript and Tailwind CSS v4 to create a polished, responsive, and engaging user interface.

### ✨ Features
- **Who's that Pokémon? Mechanics**: Guess the hidden Pokémon from a silhouette.
- **Dynamic Fetching**: Integration with the [PokéAPI](https://pokeapi.co/) via Axios to randomly select Pokémon.
- **Victory Effects**: Engaging visual feedback using `canvas-confetti` when the user guesses correctly.
- **Modern State Management**: Harnessing Pinia for a reliable, reactive global state.
- **Fully Typed**: Built strictly with TypeScript to ensure maintainability and fewer runtime errors.
- **Responsive Design**: Polished, modern UI built entirely with Tailwind CSS v4.

### 🛠️ Tech Stack
- **Framework**: [Vue 3](https://vuejs.org/) (Composition API & `<script setup>`)
- **Language**: [TypeScript](https://www.typescriptlang.org/)
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/)
- **State Management**: [Pinia](https://pinia.vuejs.org/)
- **Routing**: [Vue Router](https://router.vuejs.org/)
- **HTTP Client**: [Axios](https://axios-http.com/)
- **Build Tool**: [Vite](https://vitejs.dev/)

### 🚀 Getting Started

#### Prerequisites
- **Node.js**: v20.19.0 or >= v22.12.0
- **npm** or **yarn**

#### Installation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd pokemon-game
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Run the development server:
   ```bash
   npm run dev
   ```
4. Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 🇪🇸 Español <a name="español"></a>

### 📖 Acerca del Proyecto
Un divertido e interactivo juego al estilo "¿Quién es ese Pokémon?" creado con tecnologías web de vanguardia. Este proyecto demuestra el enfoque moderno de la *Composition API* en Vue 3, empleando TypeScript y Tailwind CSS v4 para lograr una interfaz de usuario pulida, reactiva y atractiva.

### ✨ Características Principales
- **Mecánica "¿Quién es ese Pokémon?"**: Adivina el Pokémon oculto a partir de su silueta.
- **Carga Dinámica (Fetch)**: Integración con la [PokéAPI](https://pokeapi.co/) usando Axios para seleccionar Pokémon de forma aleatoria.
- **Efectos de Victoria**: Uso de la librería `canvas-confetti` para mostrar confeti cuando aciertas el Pokémon correcto.
- **Manejo de Estado Moderno**: Uso de Pinia para un estado global reactivo, sólido y escalable.
- **Fuertemente Tipado**: Desarrollado 100% con TypeScript para asegurar la mantenibilidad y reducir errores en tiempo de ejecución.
- **Diseño Responsivo**: Interfaz moderna y estilizada construida completamente con Tailwind CSS v4.

### 🛠️ Tecnologías Utilizadas
- **Framework**: [Vue 3](https://vuejs.org/) (Composition API y `<script setup>`)
- **Lenguaje**: [TypeScript](https://www.typescriptlang.org/)
- **Estilos**: [Tailwind CSS v4](https://tailwindcss.com/)
- **Gestor de Estado**: [Pinia](https://pinia.vuejs.org/)
- **Enrutamiento**: [Vue Router](https://router.vuejs.org/)
- **Cliente HTTP**: [Axios](https://axios-http.com/)
- **Empaquetador**: [Vite](https://vitejs.dev/)

### 🚀 Cómo Empezar

#### Requisitos Previos
- **Node.js**: v20.19.0 o >= v22.12.0
- **npm** o **yarn**

#### Instalación
1. Clona el repositorio:
   ```bash
   git clone <repository-url>
   cd pokemon-game
   ```
2. Instala las dependencias:
   ```bash
   npm install
   ```
3. Inicia el servidor de desarrollo:
   ```bash
   npm run dev
   ```
4. Abre [http://localhost:5173](http://localhost:5173) en tu navegador para jugar.

---

### 📂 Project Structure / Estructura del Proyecto

```text
pokemon-game/
├── src/
│   ├── modules/
│   │   └── pokemon/          # Core game logic and components / Lógica central y componentes
│   │       ├── api/          # Axios config & PokeAPI integration / Config de Axios para PokeAPI
│   │       ├── components/   # PokemonPicture, PokemonOptions, etc.
│   │       ├── composables/  # Shared reactive logic / Lógica reactiva compartida
│   │       ├── interfaces/   # TypeScript definitions / Definiciones de TS
│   │       └── pages/        # Main game views (e.g., PokemonGame) / Vistas principales
│   ├── App.vue               # Root component / Componente raíz
│   └── main.ts               # App entry point / Punto de entrada de la app
├── package.json              # Dependencies and scripts / Dependencias y scripts
└── tsconfig.json             # TypeScript configuration / Configuración de TS
```
