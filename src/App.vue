<script setup>
import { ref, onMounted } from 'vue';
import { db } from './data/guitarras.js'
import Guitarra from './components/Guitarra.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';


// states de nuestra App con ref
const guitarras = ref([])
const carrito = ref([])

// lifecycle hook onMounted
onMounted(() => {
    guitarras.value = db
})

/**
 * Method Event "agregarCarrito"
 * Evita registros duplicados en el carrito de compra
 * @param guitarra
 */
const agregarCarrito = (guitarra) => {
    const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)
    if (existeCarrito >= 0) {
        carrito.value[existeCarrito].cantidad++
    } else {
        guitarra.cantidad = 1
        carrito.value.push(guitarra)
    }
}

// Method Event "incrementarCantidad"
const incrementarCantidad = () => {
    console.log('Más cantidad...')
}

// Method Event "decrementarCantidad"
const decrementarCantidad = () => {
    console.log('Menos cantidad...')
}

</script>

<template>
    <Header 
        :carrito="carrito" 
        @incrementar-cantidad="incrementarCantidad"
        @decrementar-cantidad="decrementarCantidad"
    />
        <!-- MAIN -->
        <main class="container-xl mt-5">
            <h2 class="text-center">Nuestra Colección</h2>
            <div class="row mt-5">
                <Guitarra 
                    v-for="guitarra in guitarras"
                    :key="guitarra.id"
                    :guitarra="guitarra"
                    @agregar-carrito="agregarCarrito"
                />
            </div>
        </main> <!-- FIN MAIN -->
    <Footer />
</template>