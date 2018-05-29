<template>
  <div>
    <h2>Nome do aniversariante</h2>
    <form @submit.prevent="generate">
      <select @change="chosenTitle = $event.target.value">
        <option v-for="title in titles" :key="title.value" :value="title.value">{{ title.label }}</option>
      </select>
      <input type="text" placeholder="Tia Maria da Conceição" @input="name = $event.target.value" />
      <button>Gerar</button>
    </form>
  </div>
</template>

<script>
export default {
  
  data() {
    return {
      name: '',
      chosenTitle: '',
      titles: [
        {
          label: 'Sr.',
          value: 'maleFormal',
        },
        {
          label: 'Sra.',
          value: 'femaleFormal',
        },
        {
          label: 'Você (h)',
          value: 'maleInformal',
        },
        {
          label: 'Você (m)',
          value: 'femaleInformal',
        },
      ],
    }
  },

  methods: {
    generate() {
      fetch(`${process.env.apiUrl}/generate`, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          name: this.name,
          title: this.chosenTitle,
        })
      })
        .then(res => res.json())
        .then(data => this.$emit('setMessage', data.message))
    },
  },
}
</script>

<style scoped>
</style>
