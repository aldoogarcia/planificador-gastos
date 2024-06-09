<script setup>
import {computed} from 'vue'
import "vue3-circle-progress/dist/circle-progress.css";
import CircleProgress from "vue3-circle-progress";
import {formatearCantidad} from '../helpers'

defineEmits(['resetear-app'])
const props= defineProps(
  {
    presupuesto: {
      type: Number,
      required: true
    },
    disponible: {
      type: Number,
      required: true
    }    ,
    gastado:{
        type:Number,
        required: true,
    }
  }
)
    
const porcentaje = computed(()=>{
    return parseInt(((props.presupuesto - props.disponible)/props.presupuesto)*100)
})

</script>
<template>
    <div class="dos-columnas">
        <div class="contenedor-grafico">
            <p class="porcentaje">{{   porcentaje }}%</p>
            <circle-progress
                :percent="porcentaje"
                :transition="1000"
                :size="250"
                :border-width="20"
                :border-bg-width="20"
                :fill-color="[porcentaje>80?'red':'blue']"
                emty-color="#f5f5f5"


            />
        </div>
        <div class="contenedor-presupuesto">
            <button 
            @click="$emit('resetear-app')"
            type="button"
            class="reset-app">
                Resetear
            </button>
            <p>
                <span>Presupuesto</span>
                 {{ formatearCantidad( presupuesto) }}
            </p>
            <p>
                <span>Disponible</span>
                 {{ formatearCantidad( disponible) }}
            </p>
            <p>
                <span>Gastado</span>
                {{ formatearCantidad(gastado) }}
            </p>

        </div>
    </div>
</template>


<style  scoped>
.dos-columnas{
    display: flex;
    flex-direction: column;
}
@media (min-width:768px){
    .dos-columnas{
        flex-direction: row;
        gap: 4rem;
        align-items: center;
    }
}
.dos-columnas  :first-child{
        margin-top: 4rem;
        align-items: center;
        margin: auto;
    }
.reset-app{
    background-color: #d65656;
    border:none;
    padding:1rem;
    width: 100%;
    color: var(--blanco);
    font-weight: 900;
    text-transform: uppercase;
    border-radius: 1rem;
    transition: background-color 300ms linear;

}

.reset-app:hover{
    cursor: pointer;
    background-color: #990404;
}
.contenedor-presupuesto{
    width: 100%;
    font-weight: 900;
}

.contenedor-presupuesto p{
    font-size: 2.4rem;
    text-align: center;
    color: var(--gris-obscuro);

}
@media(min-width:768px){
    .contenedor-presupuesto p{
        font-size: 2rem;
        text-align: left;
    }
}
.contenedor-presupuesto span{
    font-weight: 900;
    color: var(--azul);
}

.contenedor-grafico{
    position: relative;
}
.porcentaje{
    position: absolute;
    margin: auto;
    top: 40%;
    left: 0;
    right: 0;
    text-align: center;
    z-index: 100%;
    font-size: 5rem;
}
</style>