<script setup>
    import {ref} from 'vue'

    import iconCerrarModal from '../assets/img/cerrar.svg'
    import alertaItem from '../components/alerta-item.vue'


    const error=ref('')
   const emit= defineEmits(['cerrar-modal','guardar-gasto','update:nombre','update:cantidad','update:categoria'])
    const props= defineProps({
        modal:{
            type:Object,
            required:true,
        },
        nombre:{
            type:String,
            required:true,
        },
        cantidad:{
            type:[String,Number],
            required:true,
        },
        categoria:{
            type:String,
            required:true,
        },
        disponible:{
            type:Number,
            required:true,
        },
        gastado:{
            type:Number,
            required:true,
        }
    })

    const validarGasto= ()=>{
        const {nombre,cantidad,categoria} = props
        if([nombre,cantidad,categoria].includes('')){
            error.value='Todos los campos son obligatorios'
            //  console.log(error)
            setTimeout(()=>{
                error.value=''
            },3000)
            return
        }
        if(cantidad<=0){
            error.value='La cantidad debe ser mayor a 0'
            // console.log(error)
            setTimeout(() => {
                error.value='';
            },3000);
            return
        }
        if(props.cantidad>props.disponible){
            error.value='Sobrepasa el disponible'
            // console.log(error)
            setTimeout(() => {
                error.value='';
            },3000);
            return
        }

        emit('guardar-gasto',cantidad)
        
    }

</script>


<template>
    <div class="modal">
        <div class="cerrar-modal">
            <img @click="$emit('cerrar-modal')" :src="iconCerrarModal" alt="">
        </div>



        <div class="contenedor contenedor-fomulario"
            :class="[modal.muestra?'animar':'cerrar']">
        <form class="agregar-gasto"
            @submit.prevent="validarGasto"
        >
            <legend>Añadir Gasto</legend>

            <div v-if="error" class="alerta">
            <alertaItem >
                {{ error }}
            </alertaItem>
        </div>
            <div class="campo">
                <label for="nombre">Nombre del Gasto {{ modal.animar }}</label>
                <input 
                    :value="nombre" @input="$emit('update:nombre',$event.target.value)"
                    id="nombre" type="text" placeholder="Añade el nombre del gasto"
                >
            </div>
            <div class="campo">
                <label for="cantidad">Cantida</label>
                <input 
                    :value="cantidad" @input="$emit('update:cantidad',+$event.target.value)"
                id="cantidad" type="number" placeholder="Ingresa la cantidad">
            </div>
            <div class="campo">
                <label for="categoria">Cantida</label>
                <select  id="categoria"
                    :value="categoria"
                    @input="$emit('update:categoria',$event.target.value)"
                >
                    
                    <option value="">--Selecciona--</option>
                    <option value="ahorro">Ahorro</option>
                    <option value="comida">Comida</option>
                    <option value="casa">Casa</option>
                    <option value="gastos">Otros Gastos</option>
                    <option value="ocio">Ocio</option>
                    <option value="novia">Novia</option>
                    <option value="plataformas">Plataformas</option>
                </select>
            </div>
            <input type="submit">
        </form>
    </div>
    </div>


</template>



<style  scoped>
.modal{
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
    background-color: rgba(0 0 0 /0.9);
}
.cerrar-modal{
    position: absolute;
    top: 5rem;
    right: 5rem;
}
.cerrar-modal img{
    width: 3rem;
    cursor: pointer;
}

.agregar-gasto{
    position: absolute;
    margin: 0rem auto 0 auto;
    display: grid;
    gap: 2rem;
    width: 80rem;
    
}
.campo{
    display: grid;
    gap: 2rem;

}
.agregar-gasto input,
.agregar-gasto select{
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem 4rem;
    
    font-size: 2.2rem;
    width: 100%;
}

.agregar-gasto label{
    color:var(--blanco);
    font-size: 2.2rem;
} 

.agregar-gasto input[type="submit"]{
background-color: var(--azul);
color: var(--blanco)
}

.agregar-gasto legend{
    color: var(--blanco);
    margin-top: 3rem;
    font-size: 3rem;
    text-align: center;
}

.contenedor-fomulario{
    transition-property: all;
    transition-duration: 3300ms;
    transition-timing-function: ease-in;
    opacity: 0;
}
.contenedor-fomulario.animar{
    
    opacity: 1;
}
.contenedor-fomulario.cerrar{
    opacity: 0;
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
</style>