<template>
    <div class="contenedor">
        <div class="titulo">¡¡¡YA LLEGAN<br>LOS ARGENTINOS!!!</div>
        <div class="fila"><span class="numero">{{ dias }}</span><span class="etiqueta">DÍAS</span></div>
        <div class="fila"><span class="numero">{{ horas }}:{{ minutos }}:{{ segundos }}</span></div>
    </div>
</template>

<script>
export default {
    name: 'ContadorArgentinos',
    data() {
        return {
            tiempoRestante: 0,
            objetivo: new Date("2025-05-31T00:00:00"),
        };
    },
    computed: {
        dias() {
            return Math.floor(this.tiempoRestante / (1000 * 60 * 60 * 24));
        },
        horas() {
            return String(Math.floor((this.tiempoRestante / (1000 * 60 * 60)) % 24)).padStart(2, '0');
        },
        minutos() {
            return String(Math.floor((this.tiempoRestante / (1000 * 60)) % 60)).padStart(2, '0');
        },
        segundos() {
            return String(Math.floor((this.tiempoRestante / 1000) % 60)).padStart(2, '0');
        }
    },
    methods: {
        actualizarContador() {
            const ahora = new Date();
            const diff = this.objetivo - ahora;
            this.tiempoRestante = diff > 0 ? diff : 0;
        }
    },
    mounted() {
        this.actualizarContador();
        setInterval(this.actualizarContador, 1000);
    }
};
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