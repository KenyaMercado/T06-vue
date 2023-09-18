<template>
  <div id="app">
    <aside class="sidebar" :class="{ open: isSidebarOpen }">
      <button @click="toggleSidebar" class="toggle-button">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <nav class="nav-menu">
        <ul>
          <li><a href="#">Guitarras</a></li>
          <li><a href="#">Teclados</a></li>
          <li><a href="#">Baterías</a></li>
          <li><a href="#">Amplificadores</a></li>
          <li><a href="#">Accesorios</a></li>
          <li><a href="#">Todo</a></li>
          <li><a href="#acerca-de-nosotros">Acerca de Nosotros</a></li>
        </ul>
      </nav>
    </aside>
    <header class="header">
      <button @click="toggleSidebar" class="toggle-button">
        <span></span>
        <span></span>
        <span></span>
      </button>
      <h1>Perfect Chord</h1>
    </header>
    <div class="image-container">
      <transition name="slide" mode="out-in">
        <img :key="currentImage" :src="images[currentImage]" alt="Perfect Chord Image" />
      </transition>
    </div>
    <div class="best-sellers">
      <h2>Lo más vendido</h2>
      <div class="best-sellers-images">
        <div class="best-seller-item">
          <img src="@/assets/orange.jpg" alt="Producto 1" />
          <p>Crush Pro 120</p>
        </div>
        <div class="best-seller-item">
          <img src="@/assets/bcrich.jpg" alt="Producto 2" />
          <p>B.C Rich</p>
        </div>
        <div class="best-seller-item">
          <img src="@/assets/taylor.jpg" alt="Producto 3" />
          <p>Taylor 514ce</p>
        </div>
        <div class="best-seller-item">
          <img src="@/assets/mastersound.jpg" alt="Producto 4" />
          <p>Zildjian mastersound</p>
        </div>
      </div>
    </div>
    <div class="about-us" id="acerca-de-nosotros">
      <h2>Acerca de nosotros</h2>
      <p>
        Bienvenido a Perfect Chord. Somos una tienda de música en línea que ofrece una amplia gama de instrumentos musicales, desde guitarras y teclados hasta baterías y amplificadores. 
        Nuestra pasión es ayudarte a encontrar el equipo musical perfecto para tus necesidades. 
        ¡Explora nuestro catálogo y descubre la música con Perfect Chord!
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      images: [
        require('@/assets/bateria.jpg'),
        require('@/assets/guitarra.jpg'),
        require('@/assets/amplificador.jpg'),
        require('@/assets/microfono.jpg'),
      ],
      currentImage: 0,
      showImage: true,
      isSidebarOpen: false,
    };
  },
  created() {
    this.startImageAnimation();
  },
  methods: {
    startImageAnimation() {
      setInterval(() => {
        this.showImage = false;
        setTimeout(() => {
          this.currentImage = (this.currentImage + 1) % this.images.length;
          this.showImage = true;
        }, 2000); // Muestra la nueva imagen durante 2 segundos antes de cambiar
      }, 2000); 
    },
    toggleSidebar() {
      this.isSidebarOpen = !this.isSidebarOpen;
    },
  },
};

</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: black;
  font-family: 'Lato', sans-serif;
}
.about-us {
  background-color: #F6F5F2; /* Fondo blanco */
  padding: 20px;
  text-align: justify;
  
}

.about-us h2 {
  font-size: 24px;
  text-align: center;
  color: black; /* Color de texto */
}

.about-us p {
  font-size: 18px;
  color: black; /* Color de texto */
}
.header {
  background-color: #E3BD13; /* Fondo amarillo mostaza */
  text-align: center;
  font-size: 25px;
  color: white;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 20%;
  box-sizing: border-box;
  padding: 10px 0; /* Añade espacio alrededor del texto */
  z-index: 1;
}
.image-container {
  text-align: center;
  margin-top: 10%;
  overflow: hidden; 
}

/* Estilos CSS para la imagen */
img {
  max-width: 100%; 
  height: auto;
  transition: transform 2s ease; /* Duración de la animación y tipo de transición */
}

.slide-enter-active,
.slide-leave-active {
  transition: transform 2s ease; /* Duración de la animación y tipo de transición */
}

.slide-enter-to {
  transform: translateX(0); 
}

.sidebar {
  position: fixed;
  left: -300px; /* Inicialmente oculto */
  top: 0;
  height: 100%;
  width: 300px;
  background-color: #333; 
  overflow-x: hidden;
  overflow-y: auto;
  z-index: 2; 
  transition: 0.3s;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 50px;
}

.sidebar.open {
  left: 0; /* Mostrar el menú al hacer clic en el botón */
}

.toggle-button {
  position: fixed;
  left: 5px;
  top: 10px;
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.toggle-button span {
  display: block;
  width: 30px;
  height: 3px;
  background-color: white;
  margin: 6px 0;
  transition: 0.4s;
}

.toggle-button.open span:nth-child(1) {
  transform: rotate(-45deg) translate(-5px, 6px);
}

.toggle-button.open span:nth-child(2) {
  opacity: 0;
}

.toggle-button.open span:nth-child(3) {
  transform: rotate(45deg) translate(-5px, -6px);
}

/* Estilos para el menú de navegación */
.nav-menu {
  margin-top: 20px;
  color: white;
}

.nav-menu ul {
  list-style: none;
  padding: 0;
}

.nav-menu ul li {
  margin: 10px 0;
  padding: 0;
}

.nav-menu ul li a {
  text-decoration: none;
  color: white;
  font-size: 18px;
}

.header {
  background-color: #E3BD13;
  text-align: center;
  font-size: 25px;
  color: white;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 20%;
  box-sizing: border-box;
  padding: 10px 0;
}

.best-sellers {
  background-color: #000; /* Fondo blanco */
  padding: 20px;
  text-align: center;
  margin-top: 20px; /* Espacio superior */
}

.best-sellers h2 {
  font-size: 26px;
  text-align: center;
  color: white; /* Color de texto */
}

.best-sellers-images {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}

.best-seller-item {
  text-align: center;
}

.best-seller-item img {
  max-width: 100%; /* Asegura que las imágenes no sean muy grandes */
  height: auto;
  margin-bottom: 10px;
  padding: 5px; /* Espaciado alrededor de las imágenes */
  filter: grayscale(0%); /* Aplica el filtro de opacidad gris */
  transition: filter 0.3s ease;
}

.best-seller-item img:hover {
  filter: grayscale(60%); /* Elimina el filtro al pasar el mouse sobre la imagen */
}

.best-seller-item p {
  font-size: 18px;
  color: white; /* Color de texto */
}

</style>
