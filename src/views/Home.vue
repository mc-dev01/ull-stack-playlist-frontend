<template>
  <div class="container">
    <h1>Lista de reproducción</h1>
    <div class="container">
      <div class="row">
        <div class="col">
          <form @submit.prevent="agregarTema">
          <div class="form-group">
            <label class="control-label" for="tema">Ingresar canción</label>
            <div class="form-group">
              <div class="input-group mb-3">
                <div class="input-group-prepend">
                  <span class="input-group-text">🎵</span>
                </div>
                <input v-model="cancion.song" type="text"
                class="form-control" id="tema" placeholder="cancion">
                <input v-model="cancion.author" type="text"
                class="form-control" id="cantante" placeholder="cantante">
                <div class="input-group-append">
                  <button type="submit" class="btn btn-primary">Agregar</button>
                </div>
              </div>
            </div>
            </div>
          </form>
        </div>
      </div>
    </div>
    <div class="container">
      <ul class="list-group">
        <li v-for="cancion in canciones" :key="cancion._id"
        class="list-group-item d-flex justify-content-between align-items-center">
        ▶ <strong class="text-primary">{{cancion.song}}</strong>
        <span class="badge badge-primary badge-pill">{{cancion.author}}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
const API_URL = 'https://full-stack-playlist.herokuapp.com/songs';

export default {
  name: 'Home',
  data: () => ({
    canciones: [],
    cancion: {
      song: '',
      author: '',
    },
  }),
  mounted() {
    fetch(API_URL).then((res) => res.json()).then((result) => {
      this.canciones = result;
    });
  },
  methods: {
    agregarTema() {
      fetch(API_URL, {
        method: 'POST',
        body: JSON.stringify(this.cancion),
        headers: {
          'content-type': 'application/json',
        },
      }).then((res) => res.json()).then((result) => {
        this.canciones.push(result);
      });
    },
  },
};
</script>
