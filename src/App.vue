<template>
  <img alt="Vue logo" src="./assets/logo-schotten.png" class="flex-shrink-0 mx-auto my-3 bg-white max-h-40" />
  <div class="flex flex-col items-center flex-grow p-5 mx-2 bg-gray-100 content justify-items-center">
    <div class="w-full max-w-screen-md mb-5 text-left">
        <h1 class="mb-3 font-serif text-5xl ">Reparaturstatus</h1>
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

            <h2 class="mb-2 text-xl">Reparaturstatus: <span>Es tut uns leid, Ihr Auftrag ist noch in Arbeit.</span></h2>
            <p class="mb-2">Hier die Daten zum Auftrag: <span class="font-semibold">M55i9H1C07ao3J2</span></p>  
            <p class="">Kundendaten:</p> 
            <address class="mb-2 text-justify">
                Joachim Otto<br/>
                Appeldornstr. 24<br/>
                47574 Goch<br/>
                Tel: +49175-2334187
            </address>
            <p class="">
                Bestelldatum: 03.01.2022<br/>
                Ihr Auftrag: Reparatur Insignien Prinz<br/>
                Gewünschter Termin: 06.01.2022
            </p>
            <p class="mb-2">
                Vorraussichtlicher Termin der Fertigstellung: <span class="font-semibold">24.01.2022</span>
            </p>
            <p class="whitespace-pre-line">
                Bei Fragen können Sie sich gerne an uns wenden.
            </p>
            
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
    if (!code.value) {
        return;
    }

    show_clue.value = code.value == solution;
    show_error.value = code.value != solution;
};
</script>