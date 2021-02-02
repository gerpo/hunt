<template>
  <img alt="Vue logo" src="./assets/logo-schotten.png" class="mx-auto my-3 bg-white max-h-40" />
  <div class="flex flex-col items-center h-full p-5 mx-2 bg-gray-100 content justify-items-center">
    <div class="w-full mb-5 text-left">
        <h1 class="mb-3 font-serif text-5xl">Reparaturstatus</h1>
        <p>Überprüfen Sie hier den Status Ihrer Reparatur bequem mit Ihrer Auftragsnummer.</p>
    </div>
    <div id="code-box" 
        class="flex flex-wrap w-full max-w-screen-md px-10 py-5 border-2 border-gray-400 rounded shadow-md sm:flex-nowrap">

            <input type="text" 
            v-model="code" 
            @keydown.enter="checkCode"
            class="flex-grow px-5 leading-10 shadow-md sm:mr-5" >

            <button @click="checkCode" :disabled="!!disabled"
                class="w-full px-5 mt-2 font-medium leading-10 bg-gray-100 border-2 border-gray-300 rounded shadow-sm sm:mt-0 sm:w-auto hover:bg-green-100 hover:bg-opacity-20 hover:border-green-500 hover:shadow-inner">
                    Prüfen
            </button>
            
    </div>
    
    <div id="error-box" 
        v-if="show_error" 
        class="w-full max-w-screen-md px-10 py-5 mt-5 border-2 border-gray-200 rounded bg-red-50 shadow-mx">

            <h2 class="text-xl leading-relaxed">Fehler</h2>
            <p>Leider kennen wir diese Auftragsnummer nicht. Überprüfe Sie nochmal ob alles richtig eingegeben ist.</p>
            
    </div>

    <div id="clue-box" 
        v-if="show_clue" 
        class="w-full max-w-screen-md px-10 py-5 mt-5 border-2 border-gray-200 rounded bg-green-50 shadow-mx">

            <h2>Glückwunsch</h2>
            <p>Deine Bestellung ist Abholbereit.</p>
            
    </div>
    
  </div>
  <footer class="p-5 text-xs text-center">Diese Seite steht in keiner Verbindung zum Juwelier Schotten.</footer>
</template>

<script setup>
import { ref, computed } from 'vue';

const solution = 'M55i9H1C07ao3J2';
const code = ref('');
const show_error = ref(false);
const show_clue = ref(false);

let disabled = computed(() => !!!code.value);

const checkCode = () => {
    alert(code.value.length);
    if (!code.value) {
        return;
    }

    show_clue.value = code.value == solution;
    show_error.value = code.value != solution;
};
</script>