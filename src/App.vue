
<template>
  <div class="row">
    <div class="col-12 col-md-3" style="background-color: #662323;">
      <div class="container my-5">
        <img src="./assets/imgs/foxbel-music.png" alt="" class="img-fluid mx-auto d-bloc">
        <div class="mt-5 ms-4">
          <h4 class="text-light">Mi Librería</h4>
          <ul style="list-style: none;">
            <li>Recientes</li>
            <li><a href="#" @click="buscarXArtista">Artistas</a></li>
            <li><a href="#" @click="buscarXAlbum">Álbums</a></li>
            <li><a href="#" @click="buscarXCancion">Canciones</a></li>
            <li>Estaciones</li>
          </ul>

          <h4 class="text-light">Playlist</h4>
          <ul style="list-style: none;">
            <li>Metal</li>
            <li>Para Bailar</li>
            <li>Rock 90s</li>
            <li>Baladas</li>
          </ul>
        </div>

      </div>
      <!-- <BarraLateral /> -->
    </div>
    <div class="col-12 col-md-9 bg-info">
      <div class="container ">
        <div class="row mx-1 mx-md-3 my-4">
          <div class="col-7">
            <div class="input-group mb-3">
              <input type="text" class="form-control" placeholder="Buscar" v-model="texto">
              <span class="input-group-text" id="basic-addon1">@</span>
            </div>
          </div>
          <div class="col-5 text-end ">
            <h6>Usuario</h6>
          </div>
          <div class="col-12">
            <h3>Cosa</h3>
            <!-- <p>{{ texto }}</p> -->
          </div>
          <div class="col-12">
            <div v-for="cancion in canciones" :key="cancion.id">
              <!-- <h3>{{ cancion.title }}</h3> -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="row bg-danger p-5"></div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
export default {
  name: 'App',
  components: {
    HelloWorld,
  },

  data() {
    return {
      canciones: [],
      texto: ""
    }
  },

  methods: {
    async buscarXCancion() {
      try {
        const datos = await fetch("https://api.deezer.com/search/track?q=" + this.texto)
        const respuesta = await datos.json();
        this.canciones = respuesta.data;

      } catch (error) {
        this.error = error.message;
      }
    },

    async buscarXAlbum() {
      try {
        const datos = await fetch("https://api.deezer.com/search/album?q=" + this.texto)
        const respuesta = await datos.json();
        this.canciones = respuesta.data;

      } catch (error) {
        this.error = error.message;
      }
    },

    async buscarXArtista() {
      try {
        const datos = await fetch("https://api.deezer.com/search/artist?q=" + this.texto)
        const respuesta = await datos.json();
        this.canciones = respuesta.data;

      } catch (error) {
        this.error = error.message;
      }
    }
  }
}
</script>


<style>
ul li a {
  color: #fff;
  text-decoration: none;
}

ul li a:hover {
  color: #eb6060;
}

li {
  color: #fff;
}

li:hover {
  color: #eb6060;
}
</style>
