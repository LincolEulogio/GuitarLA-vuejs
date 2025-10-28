<template>
  <Header
    :carrito="carrito"
    :guitarraSeleccionada="guitarraSeleccionada"
    @agregar-carrito="agregarCarrito"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @eliminar-guitarra="eliminarGuitarra"
    @vaciar-carrito="vaciarCarrito"
  />

  <main class="container-xl mt-5">
    <h2 class="text-center">Nuestra Colección</h2>
    <div class="row mt-5">
      <Guitarra
        v-for="guitarra in guitarras"
        v-bind:guitarra="guitarra"
        @agregar-carrito="agregarCarrito"
      />
    </div>
  </main>

  <Footer />
</template>

<script setup>
import { ref, onMounted, watch } from "vue";
import { db } from "./db/guitarras";
import Guitarra from "./components/Guitarra.vue";
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

const guitarras = ref([]);
const carrito = ref([]);
const guitarraSeleccionada = ref({});

watch(
  carrito,
  () => {
    guardarCarritoStorage();
  },
  { deep: true }
);

onMounted(() => {
  guitarras.value = db;
  if (guitarras.value.length > 0) {
    guitarraSeleccionada.value = { ...guitarras.value[0] };
    cargarCarritoStorage();
  }
});

// Funcion para guardar en localStorage
const guardarCarritoStorage = () => {
  localStorage.setItem("carrito", JSON.stringify(carrito.value));
};

// Funcion para cargar desde localStorage
const cargarCarritoStorage = () => {
  const carritoGuardado = localStorage.getItem("carrito");
  if (carritoGuardado) {
    carrito.value = JSON.parse(carritoGuardado);
  }
};

// Funcion de agregar al carrito
const agregarCarrito = (guitarra) => {
  guitarraSeleccionada.value = guitarra;
  const existeCarrito = carrito.value.findIndex(
    (guitarraState) => guitarraState.id === guitarra.id
  );

  if (existeCarrito >= 0) {
    carrito.value[existeCarrito].cantidad++;
  } else {
    carrito.value.push(guitarraSeleccionada.value);
    guitarraSeleccionada.value.cantidad = 1;
  }
  guardarCarritoStorage();
};

// Funcion de incrementar cantidad en el carrito
const incrementarCantidad = (id) => {
  const index = carrito.value.findIndex((guitarra) => guitarra.id === id);
  if (carrito.value[index].cantidad >= 5) return;
  carrito.value[index].cantidad++;
};

// Funcion de decrementar cantidad en el carrito
const decrementarCantidad = (id) => {
  const index = carrito.value.findIndex((guitarra) => guitarra.id === id);
  if (carrito.value[index].cantidad <= 1) return;
  carrito.value[index].cantidad--;
};

// Funcion de eliminar guitarra del carrito
const eliminarGuitarra = (id) => {
  const index = carrito.value.findIndex((guitarra) => guitarra.id === id);
  carrito.value.splice(index, 1);
};

// Funcion de vaciar carrito
const vaciarCarrito = () => {
  carrito.value = [];
};
</script>
