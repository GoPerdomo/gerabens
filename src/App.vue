<template>
  <main>
    <h1>Gerabéns</h1>
    <div>
      <h2>Nome do aniversariante</h2>
      <form @submit.prevent="generate">
        <select @change="title = $event.target.value">
          <option v-for="title in titles" :key="title.value" :value="title.value" >{{ title.label }}</option>
        </select>
        <input type="text" placeholder="Tia Maria da Conceição" @input="name = $event.target.value" />
        <button>Gerar</button>
      </form>
      <section>
        <p>{{ message }}</p>
        <div>
          <button @click="copy">Copiar</button>
          <button>Compartilhar</button>
        </div>
      </section>
    </div>
  </main>
</template>

<script>
export default {

  data() {
    return {
      name: '',
      titles: [
        {
          label: 'Sr.',
          value: 'hFormal',
        },
        {
          label: 'Sra',
          value: 'mFormal',
        },
        {
          label: 'Você (h)',
          value: 'hInformal',
        },
        {
          label: 'Você (m)',
          value: 'mInformal',
        },
      ],
      title: '',
      message: '',
    }
  },

  created() {
    // Wake up api
    fetch(process.env.apiUrl);
  },

  methods: {
    generate() {      
      fetch(`${process.env.apiUrl}/generate`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          title: this.title,
          name: this.name,
        })
      })
        .then(res => res.json())
        .then(data => this.message = data.message)
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
  },
}
</script>

<style>
main {
  width: 50%;
  margin: auto;
}

h1 {
  text-align: center;
}

textarea {
  position: absolute;
  left: -9999px;
}
</style>
