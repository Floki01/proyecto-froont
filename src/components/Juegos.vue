<template>
    <div class="container mt-4">

        <div class="row">
            <p class="fs-1 fw-bold font-monospace text-start">Juegos</p>
            <div v-for="(juego, index) in juegos" :key="index" class="col-md-4 mb-4">

                <div class="card mb-3" style="width: 18rem;">
                    <div class="card-body">
                        <p class="card-title fs-3 fw-bold font-monospace">{{ juego.nombreJuego }}</p>
                        <p class="card-text fs-5 fw-bold font-monospace">Gratis</p>
                        <p class="card-text">{{ juego.descripcion }}</p>
                        <button class="btn btn-primary" @click="agregarJuego(juego)">Agregar</button>
                    </div>
                </div>

            </div>
        </div>

        <div class="w-50 p-3 mx-auto my-4 shadow">





            <div class="container">
                <div class="row justify-content-around">
                    <div class="col">
                        <p class="fs-1 fw-bold font-monospace text-start">Carro</p>
                    </div>

                    <div class="col">
                        
                        <div class="d-grid gap-2 d-md-flex justify-content-md-end align-items ">
                            <button type="button" class="btn btn-outline-danger" @click="vaciarCarro">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-trash" viewBox="0 0 16 16">
                                <path
                                    d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5m3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0z">
                                </path>
                                <path
                                    d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1zM4.118 4 4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4zM2.5 3h11V2h-11z">
                                </path>
                            </svg>
                            Vaciar
                        </button>
                        <button type="button" class="btn btn-primary position-relative">
                            Enviar
                            <span class="position-absolute top-0 start-100 translate-middle badge rounded-pill bg-danger">
                                {{ carro.length }}

                            </span>
                        </button>
                        </div>
                    </div>
                </div>
            </div>


            <ul class="list-group" v-for="(juego, index) in carro" :key="index">
                <li class="list-group-item">
                    <div class="container">
                        <div class="row">
                            <div class="col">
                                <p class="fw-bold font-monospace">{{ juego.nombreJuego }}</p>

                            </div>
                            <div class="col">
                                <div class="d-flex justify-content-end">
                                    <button class="btn btn-danger" @click="eliminarJuego(juego)">Eliminar</button>
                                </div>
                                
                            </div>
                        </div>
                    </div>
                </li>

            </ul>
        </div>


    </div>
</template>
  
<script>
import axios from 'axios';


export default {

    mounted() {
        this.traerJuegos();
    },

    data() {
        return {
            carro: [],
            juegos: []
        };
    },

    methods: {
        agregarJuego(juego) {
            this.carro.push(juego)
        },
        eliminarJuego(juego) {
            this.carro.pop(juego)
        },
        vaciarCarro() {
            this.carro = []
        },

        async traerJuegos() {
            await axios.get("http://localhost:8080/juegos/lista")
                .then(response => {
                    console.log(response.data)
                    this.juegos = response.data
                })
                .catch(error => {
                    console.log(error)

                });
        },

        async guardarCarro() {
            await axios.put("http://localhost:8080/juegos/guardarCarro")
                .then(response => {
                    console.log(response.data)
                    this.juegos = response.data
                })
                .catch(error => {
                    console.log(error)

                });
        },

        async traerCarros() {
            await axios.get("http://localhost:8080/juegos/lista")
                .then(response => {
                    console.log(response.data)
                    this.juegos = response.data
                })
                .catch(error => {
                    console.log(error)

                });
        }

    }
};
</script>
  

  