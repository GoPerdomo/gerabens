<template>
  <section>
    <p>{{ message }}</p>
    <div>
      <button @click="copy">Copiar</button>
      <button>Compartilhar</button>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true,
    }
  },

  methods: {
    copy() {
      // Copies the message to the clipboard
      const el = document.createElement('textarea');
      el.value = this.message;
      el.setAttribute('readonly', '');
      document.body.appendChild(el);
      el.select();
      document.execCommand('copy');
      document.body.removeChild(el);

    }
  }
}
</script>

<style scoped>
textarea {
  position: absolute;
  left: -9999px;
}
</style>
