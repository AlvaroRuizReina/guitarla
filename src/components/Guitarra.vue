<script setup>
    // Definir las props del componente
    const props = defineProps({
        guitarra: {
            type: Object,
            required: true
        }
    })

    // Declarar Component Event
    defineEmits(['agregar-carrito'])
</script>

<template>
    <!-- Componente de dinámico "Guitarras" -->
    <div class="col-md-6 col-lg-4 my-4 row align-items-center">
        <div class="col-4">
            <img class="img-fluid" 
                :src="'/img/' + guitarra.imagen + '.jpg'" 
                :alt="'imagen guitarra' + guitarra.nombre"
            >
        </div>
        <div class="col-8">
            <h3 class="text-black fs-4 fw-bold text-uppercase">{{guitarra.nombre}}</h3>
            <p>{{guitarra.descripcion}}</p>
            <p class="fw-black text-primary fs-3">{{guitarra.precio}} {{guitarra.currency}}</p>
            <button 
                type="button"
                @click="$emit('agregar-carrito', guitarra)"
                class="btn btn-dark w-100 ">Agregar al carrito
            </button>
        </div>
    </div><!-- FIN GUITARRA -->
</template>

<style lang="scss" scoped></style>