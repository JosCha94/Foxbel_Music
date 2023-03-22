<template>
    <div class="card" style="width: 10rem;">
        <img :src=" imge " class="card-img-top" :alt="titulo">
        <div class="card-body">
            <h5 class="card-title">{{ titulo }}</h5>
            <p class="card-text"><small class="text-muted">{{ artista }}</small></p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        titulo: String,
        artista: String,
        imge: String,
    }
}
</script>

    <!-- <div class="card mb-3" style="max-width: 540px;">
  <div class="row g-0">
    <div class="col-md-4">
      <img :src=" imge " class="img-fluid rounded-start" :alt="titulo">
    </div>
    <div class="col-md-8">
      <div class="card-body">
        <h5 class="card-title">{{ titulo }}</h5>
        <p class="card-text">{{ artista }}</p>
        <p class="card-text"><small class="text-muted">Last updated 3 mins ago</small></p>
      </div>
    </div>
  </div>
</div> -->