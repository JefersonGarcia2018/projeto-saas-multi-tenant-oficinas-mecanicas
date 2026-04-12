<template>
  <q-page class="flex flex-center">
    <div class="column items-center">


      <div class="q-mt-xl text-h3">
        Página Inicial
      </div>

      <div v-if="laravelData" class="q-mt-md text-grey-8 text-h5">
        Bem vindo ao Sistema de Cadastro de Produtos!
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { api } from 'boot/axios'
import { onMounted, ref } from 'vue'

// Criamos variáveis reativas para guardar os dados
const apiStatus = ref('conectando...')
const laravelData = ref(null)

onMounted(async () => {
  try {
    const response = await api.get('/v1/status')
    // Alimentamos as variáveis com o que veio do Laravel
    apiStatus.value = response.data.status
    laravelData.value = response.data
    console.log('Dados do Laravel recebidos com sucesso!')
  } catch (error) {
    apiStatus.value = 'erro'
    console.error('Erro na conexão com a API:', error)
  }
})
</script>