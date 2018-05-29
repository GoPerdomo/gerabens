<template>
  <section>
    <p>{{ message }}</p>
    <div>
      <gerabens-button kind="action" label="Copiar" @click.native="copy" />
      <gerabens-button v-if="isMobile" label="Enviar por WhatsApp" @click.native="share" />
    </div>
  </section>
</template>

<script>
import Button from '../shared/button/Button';

export default {

  components: {
    'gerabens-button': Button,
  },

  props: {
    message: {
      type: String,
      required: true,
    }
  },

  data() {
    const regex = /Android|webOS|iPhone|iPad|BlackBerry|Windows Phone|Opera Mini|IEMobile|Mobile/i;
    const isMobile = regex.test(navigator.userAgent);

    return {
      isMobile
    }
  },

  methods: {
    share() {
      window.location.href = `whatsapp://send?text=${this.message}`;
    },
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
