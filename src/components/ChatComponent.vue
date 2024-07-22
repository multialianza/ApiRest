<template>
  <div class="chat">
    <div
      v-for="(mensaje, index) in mensajes"
      :key="index"
      :style="{ backgroundColor: mensaje.color }"
      class="mensaje"
    >
      <p>{{ mensaje.usuario }}</p>
      <p>{{ mensaje.mensaje }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ChatComponent',
  props: {
    mensajes: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.chat {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: 400px;
  height: 500px;
  border: 1px solid #ccc;
  padding: 10px;
  overflow-y: auto;
}

.mensaje {
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 10px;
  max-width: 80%;
  word-wrap: break-word;
}
</style>