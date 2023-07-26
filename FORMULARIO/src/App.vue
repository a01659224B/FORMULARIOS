 <script setup>
 import{ref,computed} from 'vue'

// seccion para el primer formulario
const informacion = ref({
  parrafos:'',
})
const usuario= ref ({
nombre: '', 
apellido:'', 
sexo:'',
edad:'', 
correo:'', 
password:'',  
opciones:[], 
admin:false, 
observaciones:'',
lista:''
})

let cambio = ref(false);
let parrafo= ref(false);
let bienvenido= ref(false);
let error= ref(false);
let np = ref(0);

function mostrarDatos(event) {
  event.preventDefault();
  console.log(usuario.value);
  cambio.value = true;
}

function irainicio() {
  cambio.value = false;
}

function iraregistro() {
  error.value=false;
}

function ingresar(event) {
    event.preventDefault();
    const inicio = usuario.value;
    if (inicio.correo === user.value && inicio.password === password.value) {
      console.log('Acceso exitoso');
      parrafo.value=true
    } else {
      console.log('Error.Por favor intenta de nuevo');
      error.value=true
    }
  }

function okparrafos(event){
  event.preventDefault();
  bienvenido.value=true;
  generarParrafos();
}

const paragraphs = [];
function generarParrafos() {
    for (let i = 0; i < informacion.parrafos; i++) {
      paragraphs.push("Soy un párrafo");
    }}

</script>

<template>
  <form id="registro" v-if="!cambio"  @submit="mostrarDatos">
    <h1>Formulario de Registro</h1>
    <label for="nombre">
      Nombre 
      <br>
      <input type="text" id="nombre" v-model="usuario.nombre">
    </label>
    <br>
    <label for="apellido">Apellido
      <br>
      <input type="text" id="apellido" v-model="usuario.apellido">
    </label>
    <br>
    <label>Sexo</label>
    <br>
    <label>
      <input type="radio" name="sexo" id="femenino" value="femenino" v-model="usuario.sexo">
        Femenino
      <input type="radio" name="sexo" id="masculino" value="masculino" v-model="usuario.sexo">
        Masculino
    </label>
    <br>
    <label for="edad">Edad</label>
    <label>
      <input type="number" name="edad" id="edad" min="18" v-model="usuario.edad">
    </label>
    <br>
    <label for="correo">Correo
      <br>
      <input type="email" name="correo" id="correo" v-model="usuario.correo">
    </label>
    <br>
    <label for="password">Contraseña
      <br>
      <input type="password" id="password" v-model="usuario.password">
    </label>
    <br>
    <label>
      Conocimiento
    </label>
    <br>
    <label for="HTML"> HTML
      <input type="checkbox" id="HTML" name="opciones" v-model="usuario.opciones" value="HTML"> 
    </label>
    <label for="CSS"> CSS
      <input type="checkbox" id="CSS" name="opciones" v-model="usuario.opciones" value="CSS"> 
    </label>
    <label for="JavaScript"> JavaScript
      <input type="checkbox" id="JavaScript" name="opciones" v-model="usuario.opciones" value="JavaScript"> 
    </label>
    <label for="Vue.js"> Vue.js
      <input type="checkbox" id="Vue.js" name="opciones" v-model="usuario.opciones" value="Vue.js"> 
    </label>
    <br>
    <label for="admin"> ¿Usuario amdministrador?
      <input type="checkbox" id="admin" name="opciones" v-model="usuario.useradmin" value="admin"> 
    </label>
    <br>
    <label for="observaciones">Observaciones
    </label>
    <br>
    <textarea name="observaciones" id="observaciones" col="30" rows="10" v-model="usuario.observaciones"></textarea>
    <br>
    <label for="lista">Grupo
      <select name="lista" id="lista" v-model="usuario.lista">
        <option value="0" selected>...</option>
        <optgroup label="section 1">
        <option value="uno">1</option>
        <option value="dos">2</option>
        <option value="tres">3</option>
        </optgroup>
        <optgroup label="section 2">
        <option value="uno">1</option>
        <option value="dos">2</option>
        <option value="tres">3</option>
        </optgroup>
      </select>
    </label>   
    <br>
    <button type="submit" class="guardar">Guardar</button>
    <button type="reset" @click="restablecer">Borrar</button>
    <button class="link" @click="irainicio">Ya tengo cuenta</button>  
  </form>

  <form v-if="cambio && !bienvenido">
    <h1>Formulario ingreso</h1>
    <label for="user">Usuario
    <br>
      <input type="text" id="user" v-model="user">
    </label>
    <br>
    <label for="password">Contraseña
      <br>
      <input type="password" id="password" v-model="password">
    </label>
    <br>
    <button class="guardar" @click="ingresar">Ingresar</button>
    <button class="link" @click="iraregistro">Registrarme</button> 
  </form>

  <div v-if="parrafo && !bienvenido" >
    <form>
      <label for="parrafos">Cantidad de párrafos a mostrar
      </label>
    <label>
      <input type="number" name="parrafos" id="parrafos" min="1" v-model="informacion.parrafos">
    </label>
    <button class="guardar" @click="okparrafos">Ok</button>
    <button class="link" @click="iraregistro">Cancelar</button> 
    </form>
  </div>

  <div v-if="bienvenido" >
    <h1>Bienvenid@ {{ usuario.nombre }} {{ usuario.apellido }}</h1>
    <ul>
        <li v-for="(item,index) in usuario" :key="index">
            {{index}}:{{item}}
        </li>
    </ul>
    <br>
    <h2>Párrafos: {{ informacion.parrafos}}</h2>
    <p v-for="index in informacion.parrafos" :key="index">Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent orci sem, suscipit tempus nibh ac, rutrum ornare diam. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent orci sem, suscipit tempus nibh ac, rutrum ornare diam. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent orci sem, suscipit tempus nibh ac, rutrum ornare diam. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent orci sem, suscipit tempus nibh ac, rutrum ornare diam. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Praesent orci sem, suscipit tempus nibh ac, rutrum ornare diam. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos. {{ index}}<br> <br> </p>
  </div>

  <div v-if="error" class="alert" >
    <p>Error en usuario o contraseña. Por favor intenta de nuevo</p>
  </div>


</template>

<style>
button {
  font-size: 16px;
  font-weight: bold;
  padding: 10px 20px;
  margin: 5px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.link{
  color:darkcyan;
}

.guardar {
  font-size: 16px;
  font-weight: bold;
  padding: 10px 20px;
  margin: 5px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  background-color: green;
  color:antiquewhite;
  transition: background-color 0.3s ease;

}

h2 {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 10px;
}

h1 {
  font-size: 40 px;
  font-weight: bold;
  margin-bottom: 10px;
  text-align: center;
  background-color: darkcyan;
  color:beige
}

.alert {
  background-color: #f44336;
  color: white; 
  padding: 15px;
  margin-bottom: 20px;     
  border-radius: 4px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); 
  }

</style>