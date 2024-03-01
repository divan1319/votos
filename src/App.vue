<script setup>
import { reactive, ref } from "vue";
import Votos from "./components/Votos.vue";
import axios from "axios";

const isEditing = ref(false);
const isNew = ref(false);
const state = reactive({
  jrv: null,
  tipo: null,
});
const conteoData = ref({});

const newRegister = () => {
  isNew.value = true;
};

const searchJRV = async () => {
  await axios
    .get(
      `http://192.168.15.43:3000/api/obtener-info-jrv/?jrv=${state.jrv}&tipo_conteo=${state.tipo}`
    )
    .then((res) => {
      console.log(res.data);
      isEditing.value = true;
      isNew.value = true;
      if(res.data.conteo){
        conteoData.value = res.data.conteo;
      }else{
        conteoData.value = res.data.jrv
      }


      
    })
    .catch((err) => {
      console.log(err);
      isEditing.value = false;
      isNew.value = false;
    });
};

const reset = () => {
  state.jrv = null
  state.tipo = null

};

const refresh = ()=>{
  window.location.reload()
}
</script>

<template>

  <main class=" max-h-screen">
    <h2 class="text-center font-bold text-2xl text-white uppercase mt-10 mb-10">
      Buscar JRV
    </h2>
    <form class="max-w-md md:mx-auto mx-5 mb-7">
      <div class="flex flex-col">
        <div>
          <label
            for="default-search"
            class="mb-2 text-sm font-medium text-gray-900 sr-only dark:text-white"
            >Search</label
          >
          <div class="relative">
            <div
              class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
            >
              <svg
                class="w-4 h-4 text-gray-500 "
                aria-hidden="true"
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 20 20"
              >
                <path
                  stroke="currentColor"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="m19 19-4-4m0-7A7 7 0 1 1 1 8a7 7 0 0 1 14 0Z"
                />
              </svg>
            </div>
            <input
              v-model="state.jrv"
              type="number"
              id="default-search"
              class="block w-full p-4 ps-10 text-sm "
              placeholder="Número de JRV"
              required
            />
            <button
              type="button"
              class="text-white absolute end-2.5 bottom-2.5 bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
              @click="searchJRV"
            >
              Buscar
            </button>
          </div>
        </div>
        <div class="grid grid-cols-2 gap-3 mt-2">
          <form class="col-span-2">
            <label
              for="countries"
              class="block mb-2 text-sm font-medium text-gray-900 dark:text-white"
              >Selecciona el tipo de conteo</label
            >
            <select
              v-model="state.tipo"
              id="countries"
              class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              required
            >
              <option :value="1">Preliminar</option>
              <option :value="2">Final</option>
            </select>
          </form>

        </div>
      </div>
    </form>
    <Votos
      :editing="isEditing"
      :data="conteoData"
      :tipoConteo="state.tipo"
      @reset="reset"
    />
  </main>
</template>
