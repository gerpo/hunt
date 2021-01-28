<template>
  <img alt="Vue logo" src="./assets/SV_Viktoria_Goch_Logo.svg" class="mx-auto max-h-40" />
  <div class="flex flex-col items-center mx-2 content justify-items-center h-100">

    <div id="code-box" 
        class="flex flex-wrap w-full max-w-screen-md px-10 py-5 border-2 border-gray-400 rounded shadow-md sm:flex-nowrap">

            <input type="text" 
            v-model="code" 
            @keydown.enter="checkCode"
            class="flex-grow px-5 leading-10 shadow-md sm:mr-5" >

            <button @click="checkCode" 
                class="w-full px-5 mt-2 font-medium leading-10 bg-gray-100 border-2 border-gray-300 rounded shadow-sm sm:mt-0 sm:w-auto hover:bg-green-100 hover:bg-opacity-20 hover:border-green-500 hover:shadow-inner">
                    Prüfen
            </button>
            
    </div>
    
    <div id="error-box" 
        v-if="show_error" 
        class="w-full max-w-screen-md px-10 py-5 mt-5 border-2 border-gray-200 rounded bg-red-50 shadow-mx">

            <h2 class="text-xl leading-relaxed">Fehler</h2>
            <p>Leider kennen wir diesen Code nicht. Überprüfe nochmal ob du alles richtig eingegeben hast.</p>
            
    </div>

    <div id="clue-box" 
        v-if="show_clue" 
        class="w-full max-w-screen-md px-10 py-5 mt-5 border-2 border-gray-200 rounded bg-green-50 shadow-mx">

            <h2>Glückwunsch</h2>
            <p>Deine Bestellung ist Abholbereit.</p>
            
    </div>
    
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const solution = '2609';
const code = ref('');
const show_error = ref(false);
const show_clue = ref(false);

const checkCode = () => {
    if (!code.value) {
        return;
    }

    show_clue.value = code.value == solution;
    show_error.value = code.value != solution;
};
</script>