<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import externalComponent from "./components/externalComponent.vue";

const datos = ref([])
let pagina = Math.floor(Math.random() * 34 + 1) 

onMounted(async() => {
   await getDatos()
   setTimeout(async() => {
        pagina= Math.floor(Math.random() * 34 + 1) 
        await getDatos();
   }, 3000);
})

function hacerAlgo() {
    console.log("Se hizo click.");
}



async function getDatos(){
    try {
        const datosTransformados = []
       const respuestaa = await axios.get('https://rickandmortyapi.com/api/character/?page=' + pagina)
       //console.log(respuestaa.data.results)
       respuestaa.data.results.forEach((element) => {
            console.log(element)
            let elementoTemporal = {
                titulo: element.name,
                contenido: element.status,
                imagen: element.image,
            }
            datosTransformados.push(elementoTemporal)
       })
       console.log(datosTransformados)
       datos.value = datosTransformados
    } catch (error) {
        console.log("No se pudo acceder a la libreria remota", error.message);
    }
}

</script>

<template>
    <p class="texto">Hola Mundo</p>
    <button @click="hacerAlgo" class="boton btn btn-primary" type="button">Presione</button>
    
    <br>
    <div class="container">
        <div class="row">
            <div v-for="dato in datos" :key="dato.titulo" class="col-md-3">
                <externalComponent 
                    :imagen="dato.imagen"
                    :titulo="dato.titulo" 
                    :contenido="dato.contenido" />
            </div>
        </div>
    </div>
</template>

<style>
.texto {
    color: rgb(32, 138, 23);
    font-size: 40px;
    text-align: center;
}

.boton {
    text-align: center;
    font-size: 15px;
    display: block;
    margin: 0 auto;
}

.container {
    max-width: 100%;
    overflow: hidden;
}

.row {
    display: flex;
    flex-wrap: wrap;
}

.col-md-4 {
    display: flex;
    justify-content: center;
}

.card {
    max-width: 100%;
    height: auto;
    overflow: hidden;
}

.card-text {
    word-wrap: break-word;
    overflow-wrap: break-word;
}
</style>