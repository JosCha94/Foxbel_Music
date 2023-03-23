<script>
import Card from "./components/Card.vue";

export default {
  name: "App",
  components: {
    Card,
  },

  data() {
    return {
      canciones: [],
      texto: "",
      tipo: "",
      cancion: "",
    };
  },

  methods: {
    async buscarXCancion() {
      try {
        const datos = await fetch("https://api.deezer.com/search/track?q=" + this.texto);
        const respuesta = await datos.json();
        this.canciones = respuesta.data;
        this.tipo = "Canciones";
      } catch (error) {
        this.error = error.message;
      }
    },

    async buscarXAlbum() {
      try {
        const datos = await fetch("https://api.deezer.com/search/album?q=" + this.texto);
        const respuesta = await datos.json();
        this.canciones = respuesta.data;
        this.tipo = "Álbums";
      } catch (error) {
        this.error = error.message;
      }
    },

    async buscarXArtista() {
      try {
        const datos = await fetch("https://api.deezer.com/search/artist?q=" + this.texto);
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
    },
  },
};
</script>
<template>
  <div class="row m-0">
    <!-- MENU - BARRA LATERAL -->
    <div class="col-3 d-none d-md-block" style="background-color: #662323; height: 100vh">
      <div class="container my-5">
        <img
          src="./assets/imgs/foxbel-music.png"
          alt=""
          class="img-fluid mx-auto d-bloc"
        />
        <div class="mt-5 ms-4">
          <h4 class="text-light">Categorias</h4>
          <ul style="list-style: none">
            <li>Recientes</li>
            <li><a href="#" @click="buscarXArtista">Artistas</a></li>
            <li><a href="#" @click="buscarXAlbum">Álbums</a></li>
            <li><a href="#" @click="buscarXCancion">Canciones</a></li>
            <li>Estaciones</li>
          </ul>

          <h4 class="text-light">Playlist</h4>
          <ul style="list-style: none">
            <li>Metal</li>
            <li>Para Bailar</li>
            <li>Rock 90s</li>
            <li>Baladas</li>
          </ul>
        </div>
      </div>
    </div>
    <div class="d-md-none" style="background-color: #662323;">
      <div class="col-6 d-block d-md-none">
      <img
                src="./assets/imgs/foxbel-music.png"
                alt=""
                class="img-fluid mx-auto w-100"
            />
      </div>
      <div class="col-6 d-block d-md-none">
        <nav class="navbar navbar-light bg-transparent fixed-top" >
          <div class="container-fluid">
            <a class="navbar-brand" href="#"
              ></a>
            <button
              class="navbar-toggler"
              type="button"
              data-bs-toggle="offcanvas"
              data-bs-target="#offcanvasDarkNavbar"
              aria-controls="offcanvasDarkNavbar"
            >
              <span class="navbar-toggler-icon"></span>
            </button>
            <div
              class="offcanvas offcanvas-end text-bg-light"
              tabindex="-1"
              id="offcanvasDarkNavbar"
              aria-labelledby="offcanvasDarkNavbarLabel"
            >
              <div class="offcanvas-header" style="background-color: #662323">
                <h5 class="offcanvas-title" id="offcanvasDarkNavbarLabel">
                  <img
                    src="./assets/imgs/foxbel-music.png"
                    alt=""
                    class="img-fluid mx-auto w-50"
                  />
                </h5>
                <button
                  type="button"
                  class="btn-close btn-close-white"
                  data-bs-dismiss="offcanvas"
                  aria-label="Close"
                ></button>
              </div>
              <div class="offcanvas-body" style="background-color: #662323">
                <ul class="navbar-nav justify-content-end flex-grow-1 pe-3">
                  <li class="nav-item dropdown text-light">
                    <a
                      class="nav-link dropdown-toggle text-light"
                      href="#"
                      role="button"
                      data-bs-toggle="dropdown"
                      aria-expanded="true"
                    >
                      Categorias
                    </a>
                    <ul class="dropdown-menu dropdown-menu-dark" style="background-color: #7D3124">
                      <li>Recientes</li>
                      <li><a href="#" @click="buscarXArtista">Artistas</a></li>
                      <li><a href="#" @click="buscarXAlbum">Álbums</a></li>
                      <li><a href="#" @click="buscarXCancion">Canciones</a></li>
                      <li>Estaciones</li>
                    </ul>
                  </li>
                  <li class="nav-item dropdown text-light">
                    <a
                      class="nav-link dropdown-toggle text-light"
                      href="#"
                      role="button"
                      data-bs-toggle="dropdown"
                      aria-expanded="false"
                    >
                      PlayList
                    </a>
                    <ul class="dropdown-menu dropdown-menu-dark" style="background-color: #7D3124">
                      <li>Metal</li>
                      <li>Para Bailar</li>
                      <li>Rock 90s</li>
                      <li>Baladas</li>
                    </ul>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </nav>
      </div>
    </div>

    <!-- PRINCIPAL -->
    <div class="col-12 col-md-9" style="background-color: #f7fff2; height: 100vh">
      <div class="container" >
        <div class="row mx-1 mx-md-3 my-4">
          <div class="col-7">
            <div class="input-group mb-3">
              <input
                type="text"
                class="form-control"
                placeholder="Buscar"
                v-model="texto"
                style="
                  border-top-left-radius: 60px 60px;
                  border-bottom-left-radius: 60px 60px;
                "
              />
              <span
                class="input-group-text bg-body"
                id="basic-addon1"
                style="
                  border-top-right-radius: 60px 60px;
                  border-bottom-right-radius: 60px 60px;
                "
                ><i class="fa-solid fa-magnifying-glass" style="color: #f2f2f2"></i
              ></span>
            </div>
          </div>
          <div class="col-5 text-end">
            <h6><i class="fa-solid fa-user" style="color: #eb5757"></i> Usuario</h6>
          </div>
          <div class="col-12"></div>
          <div class="col-12">
            <h3>{{ tipo }}</h3>
            <div v-if="this.tipo === 'Álbums'">
              <div class="gap-3" id="result">
                <div v-for="cancion in canciones" :key="cancion.id">
                  <Card
                    :titulo="cancion.title"
                    :artista="cancion.artist.name"
                    :imge="cancion.cover_big"
                    :audio="cancion.preview"
                    :tipo="this.tipo"
                    :tracks="cancion.nb_tracks"
                  />
                </div>
              </div>
            </div>
            <div v-else-if="this.tipo === 'Canciones'">
              <div class="gap-3" id="result">
                <div v-for="cancion in canciones" :key="cancion.id">
                  <Card
                    :titulo="cancion.title"
                    :artista="cancion.artist.name"
                    :imge="cancion.album.cover"
                    :audio="cancion.preview"
                    :tipo="this.tipo"
                  />
                </div>
              </div>
            </div>
            <div v-else-if="this.tipo === 'Artistas'">
              <div class="gap-3" id="result">
                <div v-for="cancion in canciones" :key="cancion.id">
                  <Card
                    :titulo="cancion.name"
                    :artista="cancion.name"
                    :imge="cancion.picture_big"
                    :audio="cancion.preview"
                    :tipo="this.tipo"
                    :albums="cancion.nb_album"
                    :fans="cancion.nb_fan"
                  />
                </div>
              </div>
            </div>
            <div v-else>
              <div class="container text-center my-5">
                <div style="margin-top: 20%">
                  <h1 class="mb-4">Bienvenido a FOXBEL MUSIC</h1>
                  <marquee direction="left">
                    <p class="fw-5">
                      Para disfrutar de nuestra buena musica, escribe en la barra de
                      arriba
                      <i class="fa-solid fa-arrow-up"></i> el nombre del artista, álbum o
                      canción que deseas buscar y selecciona es la barra de la izquierda
                      <i class="fa-solid fa-arrow-left"></i> una de las categorias para
                      buscar.
                    </p>
                  </marquee>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
#app {
  font-family: Quicksand, Avenir, Helvetica, Arial, sans-serif;
}

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
.navbar {
  z-index: 1;
}
</style>
