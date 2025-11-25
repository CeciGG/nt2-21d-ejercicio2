<template>
    <div class="container-fluid mt-3" id="app">
        <input type="text" class="form-control mb-3" v-model="criterioDeBusqueda"
        placeholder="Ingresar un criterio de busqueda...">
        <input type="text" class="form-control mb-3" name="nombre" placeholder="Nombre" v-model="busquedaNombre">
        <input type="number" class="form-control" name="dni" placeholder="DNI" v-model="busquedaDNI">
        <br>
        <div class="card-deck m-0">
            <div class="row">
                <div class="col" v-for="persona in personasFiltradas">
                    <div class="card mb-3">
                        <div class="card-body">
                            <h5 class="card-title">{{getNombreCompleto(persona)}}</h5>
                            <p class="card-text">dni {{persona.dni}}</p>
                            <a href="#" class="card-link">{{persona.correo}}</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Inicio',
    data() {
        return {
            criterioDeBusqueda: '',
            busquedaNombre: '',
            busquedaDNI:'',
            personas: [
                {
                    nombre: "Daniel",
                    apellido: "Sanchez",
                    correo: "danielsanchez68@hotmail.com",
                    dni: "20442873"
                },
                {
                    nombre: "Juan",
                    apellido: "Perez",
                    correo: "j@p.gmail.com",
                    dni: "12345678"
                },
                {
                    nombre: "Ana",
                    apellido: "Suarez",
                    correo: "a@s.gmail.com",
                    dni: "87654321"
                },
                {
                    nombre: "Cecilia",
                    apellido: "Granda",
                    correo: "ceciliagranda04@gmail.com",
                    dni: "12345678"
                },
            ]
        }
    },
    computed: {
        personasFiltradas() {
            if(this.criterioDeBusqueda !== ''){
                return this.personas.filter((persona) => {
                    let registroCompleto = `${persona.nombre} ${persona.apellido} ${persona.dni} ${persona.correo}`
                    return registroCompleto.toLowerCase().includes(this.criterioDeBusqueda.toLowerCase())
                });
            }else{
                let filtroNombre = this.filtrarNombres(this.personas)
                let filtroDNI = this.filtrarDNI(filtroNombre)
                return filtroDNI
            }
            
        }
    },
    methods: {

        getNombreCompleto(persona) {
            return `${persona.nombre} ${persona.apellido}`
        },
        filtrarNombres(personas){
            if(this.busquedaNombre === '') return personas
            return personas.filter((persona) =>{
                let registroNombre = `${persona.nombre} ${persona.apellido}`
                return registroNombre.toLowerCase().includes(this.busquedaNombre.toLowerCase())
            }) 
        },
        filtrarDNI(personas){
            console.log("busqueda DNI")
            if(this.busquedaDNI === '') return personas
            return personas.filter((persona) =>{
                let registroDNI = `${persona.dni}`
                return registroDNI.toLowerCase().includes(this.busquedaDNI)
            }) 
        }
    }
}
</script>

<style scoped>
</style>