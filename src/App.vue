<script setup>
import {ref,reactive} from 'vue'
import presupuestoItem from './components/icons/presupuesto-item.vue';
import controlPresupuestoItem from './components/controlPresupuesto-item.vue';
import iconAgregarGasto from './assets/img/nuevo-gasto.svg';
import modalItem from './components/modal-item.vue'
import gastoItem from './components/gasto-item.vue'
import {generarId} from './helpers'

const modal=reactive({
  muestra:false,
  animacion:false
})
const presupuesto=ref(0);
const disponible=ref(0);
const gasto=reactive({
  nombre:'',
  cantidad:'',
  categoria:'',
  id:null,
  fecha:Date.now()
})

const gastos=ref([])

const definirPresupuesto=(cantidad)=>{
  presupuesto.value = cantidad;
}

const cambiaModal=()=>{
  modal.muestra=true
  setTimeout(()=>{
    modal.animacion=true;
  },300)
  
}

const cerrarModal=()=>{
  modal.animacion=false;
  setTimeout(()=>{
    modal.muestra=false;
  },300) 
}

const guardarGasto= ()=>{
  gastos.value.push({
    ...gasto,
    id:generarId(),
  })
  // console.log(gastos.value);
  cerrarModal();
  Object.assign(gasto,{
    nombre:'',
    cantidad:'',
    categoria:'',
    id:null,
    fecha:Date.now()
  })

}
</script>

<!-- template -->
<template>
<header>
  <h1>Planificador de Gastos</h1>
  <div class="contenedor-header contenedor sombra">
    <presupuestoItem
    v-if="presupuesto<=0"
    @definir-presupuesto="definirPresupuesto"
    />

    <controlPresupuestoItem 
    v-else
    :presupuesto="presupuesto"
    :disponible="disponible"/>
  </div>
</header>


<main v-if="presupuesto>0">

  <div class="listado-gastos contenedor">
    <h2>{{ gastos.length>0?'Gastos':'No hay gastos' }}</h2>

    <gastoItem
      v-for="gasto in gastos"
      :key="gasto.id"
      :gasto="gasto"
    />
  </div>

  <div class="crear-gasto">
    <img @click="cambiaModal" :src="iconAgregarGasto" alt="Icon Agregar Gasto">
  </div>
</main>

<div v-if="modal.muestra" class="modal">
  <modalItem
  @cerrar-modal="cerrarModal"
  @guardar-gasto="guardarGasto"
  :modal="modal"
  v-model:nombre="gasto.nombre"
  v-model:cantidad="gasto.cantidad"
  v-model:categoria="gasto.categoria"
  />
</div>

</template>

<style>
:root{
  --azul:#3b82f6;
  --blanco:#fff;
  --gris-claro:#f5f5f5;
  --gris:#94a3b8;
  --gris-obscuro:#64748b;
  --negro: #000;
}
html{
  font-size: 62.5%;
  box-sizing: border-box;

}

*,
*:before,
*:after{

  box-sizing: inherit;
}

body{
  font-size: 1.6rem;
  font-family: 'Lato','sans-serif';
  background-color: var(--gris-claro);

}
h1{
  font-size: 4rem;
}
h2{
  font-size: 3rem;
}
header{
  background-color: var(--azul);
}
header h1{
  padding:3rem 0;
  margin: 0;
  color: var(--blanco);
  text-align: center;
}

.contenedor{
  width: 90%;
  max-width: 80rem;
  margin: 0 auto;
}

.contenedor-header{
  margin-top: -5rem;
  transform: translateY(5rem);
  padding: 5rem;
}
.sombra{
  box-shadow: 0px 10px 15px -3px rgba(0,0,0,0.1);
  background-color: var(--blanco);
  border-radius: 1.5rem;
  padding: 5rem;
}
.alerta{
  padding: 1rem;
  font-weight: 900px;
  text-transform: uppercase;
  font-size: 1.6rem;
  text-align:center;
  background-color: var(--blanco);
  border-left: .5rem solid #b91c1c;
  color: #b91c1c;

}

.crear-gasto{
  position: absolute;
  bottom: 5rem;
  right: 5rem;
}
.crear-gasto img{
  width: 5rem;
  cursor: pointer;
}

.listado-gastos{
  margin-top: 15rem;
}
.listado-gastos h2{
  font-weight: 900;
  color: var(--gris-obscuro);
}
</style>
