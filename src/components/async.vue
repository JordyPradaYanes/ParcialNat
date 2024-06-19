<script setup>
import { ref } from "vue";

const carpetas = ref([{ "name": "Carpeta" }, { "name": "Carpeta" }, { "name": "Carpeta" }]);
const subcarpetas = ref([[{ "name": "Subcarpeta" }, { "name": "Subcarpeta" }, { "name": "Subcarpeta" }],
    [{ "name": "Subcarpeta" }, { "name": "Subcarpeta" }, { "name": "Subcarpeta" }],
    [{ "name": "Subcarpeta" }, { "name": "Subcarpeta" }, { "name": "Subcarpeta" }]]);

const pan = [ref(true), ref(true), ref(true)];
const indice = ref(-1);
const dos = ref(-1);
let nombre;

function cambiarIndex(index) {
    if (indice.value == index) {
        indice.value = -1
    } else {
        indice.value = index
    }
}
function añadirCar(){
    nombre=prompt("Ingrese el nombre de la carpeta");
    let uno = {"name" : nombre};
    carpetas.value.push(uno);
}
function añadirSub(i){
    nombre=prompt("Ingrese el nombre de la subcarpeta");
    let uno = {"name" : nombre};
    subcarpetas.value[i].push(uno);
}
</script>
<template>
    <div class="bg-slate-300 items-center mb-1 flex" v-for="(car, i) in carpetas" :key="i">

        <div class="m-2 items-center p-2 bg-black text-white" @click="cambiarIndex(i)">
            <button v-if="i != indice">+</button>
            <button v-else>-</button>
        </div>

        <div>
            <p class="bg-white rounded m-2 p-3 flex justify-center">{{ car.name + " "+(i+1) }}</p>

            <div class="bg-slate-300 items-center mb-1 flex justify-evenly bg-slate-200 rounded p-1 ml-5"
                v-if="i == indice" v-for="(sub, j) in subcarpetas[i]" :key="j">
                <div class="bg-white rounded p-2">
                    <p>{{ sub.name + " " + (j+1) }} </p>
                    
                </div>
            </div>

        </div>
        <div>
            <button class="flex" @click="añadirSub(i)">Añadir Carpeta</button>
        </div>
    </div>
    <div>
        <button @click="añadirCar()">Añadir Carpeta</button>
    </div>
    
</template>