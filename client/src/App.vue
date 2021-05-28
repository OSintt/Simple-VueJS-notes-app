<template>
  <div id="app">
    <div class="container">
      <discord></discord>
      <h1>{{titulo}} <b-icon icon="emoji-dizzy" ></b-icon></h1>
      <hr>
      <div class="form">
        <div class="form-group">
          <label>Nombre</label>
          <input type="text" class="form-control" v-model="inputs.nombre">
        </div>
        <div class="form-group">
          <label>Descripción</label>
          <input type="text" class="form-control" v-model="inputs.description">
        </div>
        <h6 v-if="confirm">Olvidaste rellenar un formulario!</h6>
        <button class="btn btn-primary" @click="addNote">Guardar</button>
      </div>
      <hr>
      <div class="row">
        <div class="col-lg-3 mt-4" v-for="note in notes">
          <div class="card">
            <div class="form-group">
              <h2 v-bind:style="{color: note.color, 'text-decoration': note.textDecoration}">{{note.nombre}}</h2>
              <small>
                <strong>
                id:
                </strong>
                {{note.int}}
              </small>
              <hr>
              <p>{{note.description}}</p>
              <button class="boton-tick" @click="note.color = 'green'; note.textDecoration = 'line-through';"><b-icon icon="check-square" scale="2" variant="success"></b-icon></button>
              <button class="boton-cross" @click="notes.splice(notes.indexOf(note), 1)"><b-icon icon="x-circle" scale="2" variant="danger"></b-icon></button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import discord from './components/discord';
export default {
  name: 'app',
  components: {
    discord
  },
  data () {
    return {
      titulo: "Simple Vue.js notes app!",
      confirm: false,
      inputs: {
        nombre: '',
        description: ''
      },
      notes: []
    }
  },
      methods: {
        addNote: function() {
          const { nombre, description } = this.inputs;
          if (nombre.length < 1 || description.length < 1) {
            this.confirm = true;
          } else {
            this.notes.push({
              nombre,
              description,
              color: null,
              textDecoration: null,
              int: this.notes.length + 1
            });

            this.inputs.nombre = '';
            this.inputs.description = '';
            this.confirm = false;
          }
        }
      }
}
</script>

<style>

</style>
