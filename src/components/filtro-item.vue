<script setup>
    defineProps({
        filtro:{
            type: String,
            required: true,
        }
    })
    defineEmits(['update:filtro'])
</script>

<template>
    <div class="filtro sombra contenedor">
        <form action="">
            <div class="campo">
                <label for="filtro">Selecciona por categoria</label>
                <select  id="filtro"
                    :value="filtro"
                    @input="$emit('update:filtro',$event.target.value)"
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
        </form>

    </div>
</template>


<style  scoped>
.filtro{
    margin-top: 9rem;
}
.filtro .campo{
    display: flex;
    align-items: center;
    gap: 2rem;
}
.filtro label{
    font-size: 3rem;
    font-weight: 700;
    color: var(--gris-obscuro);
}
.filtro select{
    flex: 1;
    padding: 1rem;
    border: none;
    background-color: var(--gris-claro);
    border-radius: 1rem;
    text-align: center;
    font-size: 2rem;


}
</style>