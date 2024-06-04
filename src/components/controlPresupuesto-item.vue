<script setup>
import imagen from '../assets/img/grafico.jpg'
import {formatearCantidad} from '../helpers'
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
        
</script>
<template>
    <div class="dos-columnas">
        <div class="contenedor-grafico">
            <img :src="imagen" alt="">
        </div>
        <div class="contenedor-presupuesto">
            <button class="reset-app">
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

</style>