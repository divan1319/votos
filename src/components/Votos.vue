<script setup>
import InfoVotos from './InfoVotos.vue';
import { reactive, watch, watchEffect } from "vue";

const props = defineProps({
    editing:{
        type:Boolean,
        required:true
    },
    data:{
      type:Object
    },
    tipoConteo:{
      type:Number
    }
})

const emit = defineEmits(['reset'])

const formState = reactive({
  jrv:'',
  arena:0,
  nuevas_ideas:0,
  nuestro_tiempo:0,
  fuerza_solidaria:0 ,
  fps:0,
  vamos:0,
  cd:0,
  fmln:0,
  pcn:0,
  pdc:0,
  gana:0,
  tipo_conteo:null
})

watchEffect(()=>{
  console.log(props.tipoConteo)
  formState.jrv = props?.data?.ID_JRV ?? '' 
  formState.arena = props?.data?.ARENA ?? 0
  formState.nuevas_ideas = props?.data?.NUEVAS_IDEAS ?? 0
  formState.nuestro_tiempo = props?.data?.NUESTRO_TIEMPO ?? 0
  formState.fuerza_solidaria = props?.data?.FUERZA_SOLIDARIA ?? 0
  formState.fps = props?.data?.FPS ?? 0
  formState.vamos = props?.data?.VAMOS ?? 0
  formState.cd = props?.data?.CD ?? 0
  formState.fmln = props?.data?.FMLN ?? 0
  formState.pcn = props?.data?.PCN ?? 0
  formState.pdc = props?.data?.PDC ?? 0
  formState.gana = props?.data?.GANA ?? 0
  formState.tipo_conteo = props?.tipoConteo ?? 1
})

const resetFormState = ()=>{
    emit('reset')
    Object.assign(formState,{
      jrv :'',
    arena: 0,
    nuevas_ideas: 0,
    nuestro_tiempo: 0,
    fuerza_solidaria: 0,
    fps: 0,
    vamos: 0,
    cd: 0,
    fmln: 0,
    pcn: 0,
    pdc: 0,
    gana: 0,
    tipo_conteo: null,
    })

}


</script>
<template>
 <main class=" max-h-max md:h-screen">
    
    <h2 class="text-2xl text-white font-bold text-center py-5">
      Registro de votos por JRV
    </h2>

    <div class="grid gap-6 mb-6 md:grid-cols-2 px-5 py-5  max-h-max">
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >NÚMERO JRV</label
        >
        <input
          v-model="formState.jrv"
          :disabled="editing"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="JRV"
          required
        />
      </div>
      <div>
        <label
          for="first_name"
          class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
          >ARENA</label
        >
        <input
        v-model="formState.arena"
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
          >NUEVAS IDEAS</label
        >
        <input
        v-model="formState.nuevas_ideas"
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
          >NUESTRO TIEMPO</label
        >
        <input
        v-model="formState.nuestro_tiempo"
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
          >FUERZA SOLIDARIA</label
        >
        <input
        v-model="formState.fuerza_solidaria"
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
          >FPS</label
        >
        <input
        v-model="formState.fps"
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
          >VAMOS</label
        >
        <input
        v-model="formState.vamos"
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
          >CD</label
        >
        <input
        v-model="formState.cd"
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
          >FMLN</label
        >
        <input
        v-model="formState.fmln"
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
          >PCN</label
        >
        <input
        v-model="formState.pcn"
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
          >PDC</label
        >
        <input
        v-model="formState.pdc"
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
          >GANA</label
        >
        <input
        v-model="formState.gana"
          type="number"
          id="first_name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
        />
      </div>
    </div>
    
    <InfoVotos :votos="formState" :data="props?.data" :editing="props.editing" @reset="resetFormState"/>
  </main>
</template>