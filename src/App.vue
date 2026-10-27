<script setup>
import { ref, computed } from 'vue'

const numero1 = ref(0)
const numero2 = ref(0)
const operacao = ref('soma')

const operacoes = {
  soma: { simbolo: '+', calcular: (a, b) => a + b },
  subtracao: { simbolo: '-', calcular: (a, b) => a - b },
  multiplicacao: { simbolo: '×', calcular: (a, b) => a * b },
  divisao: { simbolo: '÷', calcular: (a, b) => a / b }
}

// Recalcula sozinho sempre que um dos campos muda
const resultado = computed(() => {
  if (operacao.value === 'divisao' && numero2.value === 0) {
    return 'Não é possível dividir por zero'
  }

  const valor = operacoes[operacao.value].calcular(numero1.value, numero2.value)
  return Number.isInteger(valor) ? valor : valor.toFixed(2)
})
</script>

<template>
  <main class="calculadora">
    <h1>Calculadora</h1>

    <div class="campos">
      <input type="number" v-model.number="numero1" aria-label="Primeiro número">

      <select v-model="operacao" aria-label="Operação">
        <option v-for="(op, chave) in operacoes" :key="chave" :value="chave">
          {{ op.simbolo }}
        </option>
      </select>

      <input type="number" v-model.number="numero2" aria-label="Segundo número">
    </div>

    <p class="resultado">
      Resultado: <strong>{{ resultado }}</strong>
    </p>
  </main>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  background-color: #f0f4f8;
  color: #1f2933;
}

.calculadora {
  max-width: 480px;
  margin: 60px auto;
  padding: 32px 24px;
  background-color: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.08);
  text-align: center;
}

h1 {
  color: #42b883;
  margin-bottom: 24px;
}

.campos {
  display: flex;
  gap: 8px;
}

input,
select {
  padding: 12px;
  font-size: 18px;
  border: 1px solid #cbd2d9;
  border-radius: 8px;
}

input {
  flex: 1;
  min-width: 0;
}

.resultado {
  margin-top: 24px;
  font-size: 20px;
}

.resultado strong {
  color: #35495e;
}
</style>
