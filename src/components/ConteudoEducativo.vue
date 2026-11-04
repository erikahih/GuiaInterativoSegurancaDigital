
<script setup>
defineProps({
  titulo: {
    type: String,
    required: true
  },
  descricao: {
    type: String,
    default: ''
  },
  texto: {
    type: String,
    default: ''
  }
})

defineEmits(['voltar'])
</script>

<template>
  <section class="conteudo">
    <button class="voltar" @click="$emit('voltar')">
      ← Voltar para o início
    </button>

    <h1>{{ titulo }}</h1>

    <p class="descricao">{{ descricao }}</p>

    <div class="texto">
      <h2>Por que esse assunto é importante?</h2>
      <p>{{ texto }}</p>
    </div>
  </section>
</template>

<style scoped>
.conteudo {
  max-width: 850px;
  min-height: 65vh;
  margin: 40px auto;
  padding: 30px;
  color: #263238;
  background: #f5f7fa;
}

.voltar {
  padding: 12px 18px;
  margin-bottom: 35px;
  background: #287665;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 15px;
}

.voltar:hover {
  background: #174c45;
}

h1 {
  color: #174c45;
  font-size: 2rem;
  margin-bottom: 12px;
}

.descricao {
  color: #555;
  font-size: 1.1rem;
  line-height: 1.6;
}

.texto {
  margin-top: 30px;
  padding: 25px;
  background: #e6f1ed;
  border-radius: 12px;
  line-height: 1.8;
}

.texto h2 {
  color: #174c45;
  margin-bottom: 12px;
}

.texto p {
  color: #263238;
}
</style>
