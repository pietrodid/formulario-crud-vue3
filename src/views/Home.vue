<template>
<form @submit.prevent="procesarFormulario">
  <Input :tarea="tarea"/>
</form>
<hr>
<ListaTareas />
</template>
<script>  
import ListaTareas from '../components/ListaTareas'
import Input from '../components/Input'
import {mapActions} from 'vuex'
const shortid = require('shortid'); 

export default {
  name: 'Home',
  components: {
    Input,
     ListaTareas
    
  },
  data() {
    return {
      texto: '',
      tarea: {
        id: '',
        nombre: '',
        categorias: [],
        estado: '',
        numero: 0
      }
    }
  },
  methods: {
    ...mapActions(['setTareas']),

    procesarFormulario(){
      console.log(this.tarea)
      if(this.tarea.nombre.trim() === "") {
        console.log('campo vacio')
        return
      }
      console.log('no está vacio')
      
      // generar id
      this.tarea.id = shortid.generate()
      console.log(this.tarea.id)
      // envian datos

      this.setTareas(this.tarea)

      this.tarea =  {
        id: '',
        nombre: '',
        categorias: [],
        estado: '',
        numero: 0
      }
    }
  },
  computed: {
      }
}
</script>
