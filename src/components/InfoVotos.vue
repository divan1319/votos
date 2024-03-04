<script setup>
import { reactive, watchEffect } from 'vue';
import {useToast} from "vue-toastification"
import axios from "axios"
const toast = useToast()
const props = defineProps({
  votos:{
    type:Object,
    required:true
  },
  editing:{
    type:Boolean,
    required:true
  },
  data:{
    type:Object,
  }
})

const emit = defineEmits(['reset'])

const state = reactive({
  total_papeletas:0,
  nulos:0,
  impugnados:0,
  abstenciones:0,
  faltantes:0,
  sobrantes:0,
  inutilizadas:0,
  entregadas_votantes:0
})

const validationData = () =>{
  if(props.votos.jrv == '' || props.votos.jrv == null) return 'Tienes que enviar el número de la JRV'
  return false
}

const sendData = async()=>{
    const verify = validationData()
    if(verify){
      toast.error(verify)
      return
    }

    props.votos.total_papeletas = state.total_papeletas
    props.votos.nulos = state.nulos
    props.votos.impugnados = state.impugnados
    props.votos.abstenciones = state.abstenciones
    props.votos.faltantes = state.faltantes
    props.votos.sobrantes = state.sobrantes
    props.votos.inutilizadas = state.inutilizadas
    props.votos.entregadas_votantes = state.entregadas_votantes

    await axios.post('http://192.168.15.43:3000/api/registrar-votos-jrv',props.votos)
    .then(()=>{  
      toast.success('Datos guardados')
      
    })
    .catch(()=> toast.error('Error al registrar los votos'))
    .finally(()=> {
      emit('reset')
    })
}

watchEffect(()=>{
  state.total_papeletas = props?.data?.TOTAL_PAPELETAS ?? 0
  state.nulos = props?.data?.NULOS ?? 0
  state.impugnados = props?.data?.IMPUGNADOS ?? 0
  state.abstenciones = props?.data?.ABSTENCIONES ?? 0
  state.faltantes = props?.data?.FALTANTES ?? 0
  state.sobrantes = props?.data?.SOBRANTES ?? 0
  state.inutilizadas = props?.data?.INUTILIZADAS ?? 0
  state.entregadas_votantes = props?.data?.ENTREGADAS_VOTANTES ?? 0
})
</script>
<template>
  <div class="max-h-max">
    <h2 class="text-2xl  font-bold text-center py-5">
      Resumen Papeletas
    </h2>
    <div class="grid gap-6 mb-6 md:grid-cols-2 px-5 py-5  max-h-max">
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >TOTAL PAPELETAS</label
        >
        <input
        v-model="state.total_papeletas"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          
          required
        />
      </div>

      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >NULOS</label
        >
        <input
        v-model="state.nulos"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >IMPUGNADOS</label
        >
        <input
        v-model="state.impugnados"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >ABSTENCIONES</label
        >
        <input
        v-model="state.abstenciones"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >FALTANTES</label
        >
        <input
        v-model="state.faltantes"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >SOBRANTES</label
        >
        <input
        v-model="state.sobrantes"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >INUTILIZADAS</label
        >
        <input
        v-model="state.inutilizadas"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >ENTREGADAS VOTANTES</label
        >
        <input
        v-model="state.entregadas_votantes"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="John"
          required
        />
      </div>
    </div>
    <button
      type="submit"
      class="text-white w-3/4 md:w-40 mx-12 md:mx-5 bg-gradient-to-r from-cyan-500 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-7"
      @click="sendData"
    >
      Guardar
    </button>
  </div>
</template>
