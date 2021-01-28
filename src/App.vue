<template>
  <img alt="Vue logo" src="./assets/SV_Viktoria_Goch_Logo.svg" class="mx-auto max-h-40" />
  <div class="content flex justify-items-center items-center h-100 flex-col">
    <div id="code-box" class="flex w-full max-w-screen-md rounded shadow-md border-gray-400 border-2 px-10 py-5">
      <input type="text" class="flex-grow shadow-md px-5 mr-5 leading-10" v-model="code" @keydown.enter="checkCode">
      <button class="hover:bg-green-200 hover:shadow-inner bg-gray-100 rounded shadow-sm leading-10 px-5" @click="checkCode">Prüfen</button>
    </div>
    <div id="error-box" v-if="show_error" class="bg-red-50 mt-5 w-full max-w-screen-md rounded shadow-mx border-2 border-gray-200 px-10 py-5">
      <h2 class="leading-relaxed text-xl">Fehler</h2>
      <p>Leider kennen wir diesen Code nicht. Überprüfe nochmal ob du alles richtig eingegeben hast.</p>
    </div>
    <div id="clue-box" v-if="show_clue" class="bg-red-50 mt-5 w-full max-w-screen-md rounded shadow-mx border-2 border-gray-200 px-10 py-5">
      <h2>Glückwunsch</h2>
      <p>Deine Bestellung ist Abholbereit.</p>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const solution = '2609';
const code = ref('');
const show_error = ref(false);
const show_clue = ref(false);

const checkCode = () => {
  if (!code.value) {
    return;
  }

  show_clue.value = code.value == solution
  show_error.value = code.value != solution
}
</script>