<template>
  <div id="app">
    <div v-if="loading">Cargando...</div>
    <div v-else class="container">
      <div class="user">
        <img :src="usuario1.picture.large" :alt="usuario1.name.first" />
        <p>{{ usuario1.name.first }} {{ usuario1.name.last }}</p>
        <input v-model="nuevoMensaje1" placeholder="Escribe un mensaje..." />
        <button @click="agregarMensaje(usuario1, nuevoMensaje1, '#007bff')">
          Enviar
        </button>
      </div>
      <ChatComponent :mensajes="mensajes" />
      <div class="user">
        <img :src="usuario2.picture.large" :alt="usuario2.name.first" />
        <p>{{ usuario2.name.first }} {{ usuario2.name.last }}</p>
        <input v-model="nuevoMensaje2" placeholder="Escribe un mensaje..." />
        <button @click="agregarMensaje(usuario2, nuevoMensaje2, '#dc3545')">
          Enviar
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ChatComponent from './components/ChatComponent.vue';

export default {
  name: 'App',
  components: {
    ChatComponent,
  },
  data() {
    return {
      usuario1: null,
      usuario2: null,
      nuevoMensaje1: '',
      nuevoMensaje2: '',
      mensajes: [],
      loading: true,
    };
  },
  mounted() {
    this.obtenerUsuarios();
  },
  methods: {
    obtenerUsuarios() {
      axios
        .get('https://randomuser.me/api/?results=2')
        .then((response) => {
          this.usuario1 = response.data.results[0];
          this.usuario2 = response.data.results[1];
          this.loading = false;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    agregarMensaje(usuario, mensaje, color) {
      if (mensaje.trim() !== '') {
        this.mensajes.push({
          usuario: `${usuario.name.first} ${usuario.name.last}`,
          mensaje,
          color,
        });
        this.nuevoMensaje1 = '';
        this.nuevoMensaje2 = '';
      }
    },
  },
};
</script>

<style>
/* Estilos CSS */
</style>