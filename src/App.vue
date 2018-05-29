<template>
  <div>
    <gerabens-header />
    <main>
      <gerabens-formulary @setMessage="message = $event"/>
      <gerabens-generated :message="message" />
    </main>
  </div>
</template>

<script>
import Header from './components/header/Header.vue';
import Formulary from './components/formulary/Formulary.vue';
import Generated from './components/generated/Generated.vue';

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
</style>
