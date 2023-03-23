<script>
export default {
  name: "Card",
  data() {
    return {
      activo: "",
    };
  },
  props: {
    titulo: String,
    artista: String,
    imge: String,
    audio: String,
    tipo: String,
    tracks: String,
    albums: String,
    fans: String,
  },
};
</script>

<template>
  <a href="#" class="btn" @click="this.activo = 'si'" title="escuchar/ ver">
    <div class="card" style="width: 10rem">
      <img :src="imge" class="card-img-top" :alt="titulo" />
      <div class="card-body text-start" style="height: 8rem">
        <h5 class="card-title fs-6">{{ titulo }}</h5>
        <p class="card-text">
          <small class="text-muted">{{ artista }}</small>
        </p>
      </div>
    </div>
  </a>
  <!-- CANIONES -->
  <div v-if="tipo === 'Canciones'">
    <div
      class="row p-4 fixed-bottom"
      style="background-color: #eb5757"
      v-show="this.activo != ''"
    >
      <div class="col-11">
        <div class="row">
          <audio controls>
            <source :src="audio" type="audio/mpeg" />
          </audio>
        </div>
      </div>
      <div class="col-1 d-flex justify-content-center align-items-center">
        <button type="button" @click="this.activo = ''" class="btn-close"></button>
      </div>
    </div>
  </div>
  <!-- ALBUMS -->
  <div v-if="tipo === 'Álbums'">
    <div
      class="row p-3 fixed-bottom"
      style="background-color: #eb5757"
      v-show="this.activo != ''"
    >
      <div class="col-12 col-md-11">
        <div class="row d-flex justify-content-center">
          <div class="card" style="max-width: 540px">
            <div class="row g-0">
              <div class="col-md-4">
                <img :src="imge" class="img-fluid rounded-start" :alt="titulo" />
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5 class="card-title">{{ titulo }}</h5>
                  <p class="card-text">
                    Artista: {{ artista }}
                    <br />
                    Canciones: {{ tracks }}
                  </p>
                  <p class="card-text">
                    <small class="text-muted">Last updated 3 mins ago</small>
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="col-12 col-md-1 mt-4 mt-md-0 d-flex justify-content-center align-items-center">
        <button type="button" @click="this.activo = ''" class="btn-close"></button>
      </div>
    </div>
  </div>
  <!-- ARTISTAS -->
  <div v-if="tipo === 'Artistas'">
    <div
      class="row p-3 fixed-bottom"
      style="background-color: #eb5757"
      v-show="this.activo != ''"
    >
      <div class="col-12 col-md-11">
        <div class="row d-flex justify-content-center">
          <div class="card" style="width: 18rem">
            <img :src="imge" class="card-img-top mt-2" :alt="titulo" />
            <div class="card-body">
              <h5 class="card-title">{{ titulo }}</h5>
              <p class="card-text">
                Albunes compuestos: {{ albums }}
                <br />
                Número de fans: {{ fans }}
              </p>
            </div>
          </div>
        </div>
      </div>
      <div class="col-12 col-md-1 d-flex justify-content-center align-items-center mt-4 mt-md-0">
        <button type="button" @click="this.activo = ''" class="btn-close"></button>
      </div>
    </div>
  </div>
</template>

<style>
q {
  text-align: right;
}
</style>
