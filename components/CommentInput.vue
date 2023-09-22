<template>
  <form class="comment-form" @submit.prevent="submitForm">
    <legend>Comentar</legend>
    <label for="name">Nombre</label>
    <input id="name" v-model="name" type="text" required />
    <label for="email">Correo</label>
    <input id="email" v-model="email" type="email" />
    <label for="content">Comentario</label>
    <textarea
      id="content"
      v-model="content"
      cols="30"
      rows="4"
      placeholder="Escribe tu comentario"
      required
    ></textarea>
    <button type="submit">Comentar</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
      content: '',
    }
  },
  methods: {
    submitForm() {
      this.$emit('submitForm', {
        name: this.name,
        email: this.email,
        content: this.content,
      })
      this.name = ''
      this.email = ''
      this.content = ''
    },
  },
}
</script>

<style lang="scss" scoped>
.comment-form {
  @apply flex flex-col gap-2 mt-6 mb-4;
  legend {
    @apply text-xl font-bold;
  }
  label {
    @apply text-gray-600;
  }
  input,
  textarea {
    @apply p-2;
  }
  button {
    @apply border bg-gray-300 hover:bg-gray-400 px-4 py-2 text-center font-bold;
  }
}
</style>
