<template>
    <div class="contenedor">
        <div class="titulo">¡¡¡YA LLEGAN<br>LOS ARGENTINOS!!!</div>
        <div v-if="dias > 0">
            <div class="fila"><span class="numero">{{ dias }}</span><span class="etiqueta">DÍAS</span></div>
            <div class="fila"><span class="numero">{{ horas }}:{{ minutos }}:{{ segundos }}</span></div>
        </div>
        <div v-else-if="dias === 0">
            <div class="fila"></div>
            <img src="/plane.avif" alt="Plane" class="plane-image" />
            <br />
            <span class="etiqueta">VIAJANDO</span>
        </div>
        <div v-else>
            <div class="fila">
                <span class="etiqueta">DISFRUTANDO COLOMBIA</span>
            </div>
            <div class="fila">
                <a href="https://photos.app.goo.gl/M9rtxq2txrPoQ4YQ8" target="_blank" class="boton etiqueta">
                    ¡Sube tus fotos con nosotros aquí!
                </a>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue';

const tiempoRestante = ref(0);
const objetivo = new Date("2025-05-31T21:00:00");

const dias = computed(() => Math.floor(tiempoRestante.value / (1000 * 60 * 60 * 24)));
const horas = computed(() => String(Math.floor((tiempoRestante.value / (1000 * 60 * 60)) % 24)).padStart(2, '0'));
const minutos = computed(() => String(Math.floor((tiempoRestante.value / (1000 * 60)) % 60)).padStart(2, '0'));
const segundos = computed(() => String(Math.floor((tiempoRestante.value / 1000) % 60)).padStart(2, '0'));

const actualizarContador = () => {
    const ahora = new Date();
    const diff = objetivo - ahora;
    tiempoRestante.value = diff;
};

onMounted(() => {
    actualizarContador();
    setInterval(actualizarContador, 1000);
});
</script>

<style scoped>
.contenedor {
    background-color: #b30000;
    color: white;
    font-family: Arial, sans-serif;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    padding: 20px;
}

.titulo {
    font-size: 12vw;
    font-weight: bold;
    text-transform: uppercase;
    margin-bottom: 2rem;
    line-height: 1.2;
}

.fila {
    display: flex;
    align-items: baseline;
    justify-content: center;
    margin: 10px 0;
}

.numero {
    font-size: 14vw;
    font-weight: bold;
    margin-right: 10px;
}

.etiqueta {
    font-size: 13vw;
    font-weight: bold;
    text-transform: uppercase;
}

.boton {
    display: inline-block;
    background-color: #ffffff;
    color: #b30000;
    text-decoration: none;
    font-weight: bold;
    padding: 10px 20px;
    border-radius: 5px;
    border: 2px solid #b30000;
    transition: background-color 0.3s, color 0.3s;
    text-transform: uppercase;
}

.boton:hover {
    background-color: #b30000;
    color: #ffffff;
}

@media (min-width: 768px) {
    .titulo {
        font-size: 4vw;
    }

    .numero {
        font-size: 8vw;
    }

    .etiqueta {
        font-size: 2.5vw;
    }
}
</style>