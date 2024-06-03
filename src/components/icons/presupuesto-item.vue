<script setup>
import {ref} from 'vue'
import alertaItem from '../alerta-item.vue';

const mensaje=ref('')
const numero =ref(0)

const emit= defineEmits(['definir-presupuesto'])
const validarPresupuesto=()=>{
    if(numero.value<=0 || numero.value===null){
        // console.log("invalido")
        // console.log(mensaje)
        mensaje.value="El presupuesto no puede ser negativo o cero"
        numero.value=null
        setTimeout(()=>{
            mensaje.value='';
        },3000)
    }

    emit('definir-presupuesto',numero.value)
}




</script>

<template>

<div v-if="mensaje" class="alerta">
      <alertaItem>
        {{ mensaje }}
      </alertaItem>
  
  </div>


    <form class="presupuesto" @submit.prevent="validarPresupuesto">
        <div class="campo">
            <label for="nuevo-presupuesto">Nuevo presupuesto</label>
            <input type="number"
                id="nuevo-presupuesto"
                class="nuevo-presupuesto"
                placeholder="Ingresa tu Presupuesto"
                v-model="numero"
            >
        </div>
        <input type="submit" value="Definir Presupuesto" name="" id="">
    </form>
</template>



<style  scoped>
    .presupuesto{
        width: 100%;

    }
    .campo{
        display: grid;
        gap: 2rem;
    }
    .presupuesto input[type="number"]{
        background-color: var(--gris-claro);
        border-radius: 1rem;
        padding: 1rem;
        border: none;
        font-size: 2.2rem;
        text-align: center;

    }

    .presupuesto input[type="submit"] {
        background-color: var(--azul);
        border-radius: 1rem;
        padding: 1rem;
        border: none;
        font-size: 2rem;
        text-align: center;
        margin-top: 2rem;
        color: var(--blanco);
        font-weight: 900;
        width: 100%;
        transition: background-color 200ms linear; 
    }
    .presupuesto input[type="submit"]:hover{
        background-color: #1048a4;
        cursor: pointer;
    }
    .presupuesto label{
        font-size: 2.3rem;
        text-align: center;
        color:var(--azul)
    }
</style>