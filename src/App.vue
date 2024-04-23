<template>
  <div id="app">
    <h1>{{ nombreLista }}</h1>
    <input v-model="nombreLista" placeholder="Nombre de la lista" />
    <ul>
      <li v-for="(tarea, index) in tareas" :key="index">
        <span v-if="!tarea.editing">{{ tarea.text }}</span>
        <input v-else v-model="tarea.text" />
        <button @click="eliminarTarea(index)">Eliminar</button>
        <button @click="alternarEdicion(index)">
          {{ tarea.editing ? 'Guardar' : 'Modificar' }}
        </button>
      </li>
    </ul>
    <input v-model="nuevaTarea" placeholder="Nueva tarea" />
    <button @click="agregarTarea">Agregar tarea</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombreLista: 'Mi lista de tareas',
      tareas: [
        { text: 'Primera tarea de prueba', editing: false },
      ],
      nuevaTarea: '',
    };
  },
  methods: {
    agregarTarea() {
      if (this.nuevaTarea.trim() !== '') {
        this.tareas.push({ text: this.nuevaTarea, editing: false });
        this.nuevaTarea = '';
      }
    },
    eliminarTarea(index) {
      this.tareas.splice(index, 1);
    },
    alternarEdicion(index) {
      this.tareas[index].editing = !this.tareas[index].editing;
    },
  },
};
</script>

<style>
  #app{
    background-color: rgb(213, 106, 106);
    border-radius: 100px;
  }
  body{
    background-image: url('./assets/background-to-do-list.jpg');
  }
</style>
