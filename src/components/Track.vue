<template>
  <div class="card">
    <figure class="image is-4by4">
      <img :src="track.album.images[1].url">
    </figure>
    <div class="card-content">
      <div class="media">
        <div class="media-left">
          <figure class="image is-48x48">
            <img :src="track.album.images[1].url">
          </figure>
        </div>
        <div class="media-content">
          <p class="title is-6"><strong>{{track.name}}</strong></p>
          <p class="subtitle is-6">{{track.artists[0].name}}</p>
        </div>
      </div>
      <div class="content" >
        <small >{{track.duration_ms}}</small>
        <div class="has-text-centered">
          <a href="#">
            <span class="icon">
              <i class="fa fa-play" @click="selectTrack"></i>
            </span>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
  export default {
    props: {
      track:{ type: Object, required:true}
  },

    methods: {
      selectTrack() {
        this.$emit('select', this.track.id)
      }
    }
}
</script>
