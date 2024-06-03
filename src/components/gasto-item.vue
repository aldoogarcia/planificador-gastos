<script setup>
import {  formatearCantidad, formatearFecha,} from '@/helpers';
import IconoAhorro from '../assets/img/icono_ahorro.svg'
    import IconoCasa from '../assets/img/icono_casa.svg'
    import IconoComida from '../assets/img/icono_comida.svg'
    import IconoGastos from '../assets/img/icono_gastos.svg'
    import IconoOcio from '../assets/img/icono_ocio.svg'
    import IconoSalud from '../assets/img/icono_salud.svg'
    import IconoNovia from '../assets/img/icono_novia.svg'
    import IconoSuscripciones from '../assets/img/icono_suscripciones.svg'



    const diccionarioIconos = {
        ahorro : IconoAhorro,
        comida : IconoComida,
        casa : IconoCasa,
        gastos : IconoGastos,
        ocio : IconoOcio,
        salud : IconoSalud,
        plataformas : IconoSuscripciones,
        novia:IconoNovia
    }
defineProps({
    gasto:{
        type: Object,
        required: true,
    }
})

</script>

<template>
    <div class=" gasto sombra">
        <div class="contenido">
            <img class="icono" :alt="gasto.categoria" :src="diccionarioIconos[gasto.categoria]">
            <div class="detalles">
                <p class="categoria">{{gasto.categoria  }}</p>
                <p class="nombre">{{ gasto.nombre }}</p>
                <p class="fecha">{{formatearFecha(gasto.fecha) }}</p>
            </div>

        </div>
        <p class="cantidad">{{ formatearCantidad(gasto.cantidad) }}</p>
    </div>
</template>



<style scoped>
    .gasto{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 2rem;
    }
    .contenido{
        display: flex;
        align-items: center;
        gap :4rem;
    }
    .detalles{
        margin:0 0 2rem 0;

    }
    .nombre{
        color:var(--gris-oscuro);
        font-size: 2.2rem;
        font-weight: 700;
        cursor: pointer;
    }
    .categoria{
        color: var(--gris);
        font-size: 2rem;
        text-transform: uppercase;
        font-weight: 900;
    }
    .fecha{
        color:var(--gris-oscuro);
        font-size: 2.2rem;
        font-weight: 700;
    }
    .icono{
        width: 7rem;
    }
    .cantidad{
        margin: 0;
        font-size: 4rem;
        font-weight: 900;
    }
</style>