<template>
  <div>
    <gerabens-header />
    <main>
      <gerabens-formulary @setMessage="message = $event" />
      <transition name="generate">
        <gerabens-generated v-if="message" :message="message" />
      </transition>
    </main>
  </div>
</template>

<script>
import Header from './components/header/Header';
import Formulary from './components/formulary/Formulary';
import Generated from './components/generated/Generated';

export default {

  components: {
    'gerabens-header': Header,
    'gerabens-formulary': Formulary,
    'gerabens-generated': Generated,
  },

  data() {
    return {
      message: '',
    }
  },

  created() {
    // Wake up api
    fetch(process.env.apiUrl);
  },
}
</script>

<style scoped>
main {
  width: 50%;
  margin: auto;
}

.generate-enter {
  opacity: 0;
}

.generate-enter-active {
  transition: opacity 1s;
}
</style>
