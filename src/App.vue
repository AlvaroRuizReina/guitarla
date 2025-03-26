<script setup>
import { ref, onMounted } from 'vue';
import { db } from './data/guitarras.js'
import Guitarra from './components/Guitarra.vue';
import Header from './components/Header.vue';
import Footer from './components/Footer.vue';


// states de nuestra App con ref
const guitarras = ref([])
const guitarra = ref({})
const carrito = ref([])

// lifecycle hook onMounted
onMounted(() => {
    guitarras.value = db
    guitarra.value = db[3]
})

/**
 * Computed Event "incrementarCantidad"
 * Incrementa la cantidad de elementos añadir al carrito de compra
 * @param id
 * @argument id
 * @argument producto
 */
const incrementarCantidad = id => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    if(carrito.value[index].cantidad >= 10) return
    carrito.value[index].cantidad++
}

/**
 * Computed Event "decrementarCantidad"
 * Reduce la cantidad de elementos añadir al carrito de compra
 * @param id
 * @argument id
 * @argument producto
 */
const decrementarCantidad = id => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    if(carrito.value[index].cantidad <= 1) return
    carrito.value[index].cantidad--
}

/**
 * Computed Event "vaciarCarrito"
 * vaciar carrito de compra
 * @param id
 * @argument id
 * @argument producto
 */
const vaciarCarrito = () => {
    carrito.value = []
}

/**
 * Method Event "agregarCarrito"
 * Evita registros duplicados en el carrito de compra
 * @param guitarra
 */
const agregarCarrito = guitarra => {
    const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)
    if (existeCarrito >= 0) {
        carrito.value[existeCarrito].cantidad++
    } else {
        guitarra.cantidad = 1
        carrito.value.push(guitarra)
    }
}

/**
 * Method Event "elimiarProducto"
 * Elimina un producto individual del carrito de compra
 * @param id
 * @argument id
 * @argument producto
 */
const elimiarProducto = id => {
    carrito.value = carrito.value.filter(producto => producto.id != id)
}
</script>

<template>
    <Header 
        :carrito="carrito"
        :guitarra="guitarra"
        @incrementar-cantidad="incrementarCantidad"
        @decrementar-cantidad="decrementarCantidad"
        @agregar-carrito="agregarCarrito"
        @eliminar-producto="elimiarProducto"
        @vaciar-carrito="vaciarCarrito"
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