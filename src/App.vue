<script>
import HelloWorld from './components/HelloWorld.vue';
import Card from './components/Card.vue';
export default {
  name: 'App',
  components: {
    HelloWorld,
    Card
  },

  data() {
    return {
      canciones: [],
      texto: "",
      tipo: "",
      audio: "",
      audio2: ""
    }
  },

  methods: {
    async buscarXCancion() {
      try {
        const datos = await fetch("https://api.deezer.com/search/track?q=" + this.texto)
        const respuesta = await datos.json();
        this.canciones = respuesta.data;
        this.tipo = "Canciones";

      } catch (error) {
        this.error = error.message;
      }
    },

    async buscarXAlbum() {
      try {
        const datos = await fetch("https://api.deezer.com/search/album?q=" + this.texto)
        const respuesta = await datos.json();
        this.canciones = respuesta.data;
        this.tipo = "Álbums";

      } catch (error) {
        this.error = error.message;
      }
    },

    async buscarXArtista() {
      try {
        const datos = await fetch("https://api.deezer.com/search/artist?q=" + this.texto)
        const respuesta = await datos.json();
        this.canciones = respuesta.data;
        this.tipo = "Artistas";

      } catch (error) {
        this.error = error.message;
      }
    },

    async agregarAudio() {
      try {
        this.audio = this.audio2;
      } catch (error) {
        this.error = error.message;
      }
    }
  }
}
</script>
<template>
  <div class="row m-0">
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


          </div>
          <div class="col-12" id="result">
            <h3>{{ tipo }}</h3>
            <h3>{{ audio }}</h3>
            <div class="gap-3" id="result">

              <div v-for="cancion in canciones" :key="cancion.id">
                
                  <Card :titulo="cancion.title" :artista="cancion.artist.name" :imge="cancion.cover" />
                <!-- <input type="hidden" :value="cancion.previe">
<button @click="agregarAudio">Escuchar</button> -->
                <!-- <Card :titulo="cancion.name" :artista="cancion.name" :imge="cancion.picture" /> -->
              </div>

            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div class="row bg-danger p-4 fixed-bottom">
    <audio controls>
      <source :src="audio" type="audio/mpeg">
    </audio>

  </div>
</template>

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

#result {
  display: flex;
  flex-wrap: wrap;
}
</style>
