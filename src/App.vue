<template>
  <div id="app">
    <pm-header></pm-header>
    <pm-notification v-show="showNotification"></pm-notification>
    <pm-loader v-show="isLoading"></pm-loader>
    <section class="section" v-show="!isLoading">
      <div class="container">
        <div class="field">
          <p class="control">
            <input class="input is-large" type="text" placeholder="Busca Tu Canción" @keyup.enter="search" v-model="schQ">
            <p class="subtitle rslt">{{total}}</p>
            <div class="btnS">
              <a class="button is-success" @click="search" >
                <span class="icon is-small">
                  <i class="fa fa-search"></i>
                </span>
                <span>Buscar</span>
              </a>
              <a class="button is-danger ">
                <span class="icon is-small">
                  <i class="fa fa-remove"></i>
                </span>
              </a>
            </div>
          </p>
        </div>
      </div>
      <div class="container rltC">
        <div class="columns is-multiline">
          <div class="column is-one-quarter" v-for="t in tracks">
            <pm-track :track="t" v-on:select="setSelectedTrack" :class="{'is-active': t.id == selectedTrack}"></pm-track>
          </div>
        </div>
      </div>
    </section>
    <pm-footer></pm-footer>
  </div>
</template>

<script>
import trackService from '@/services/track'
import PmFooter from '@/components/layout/Footer.vue'
import PmHeader from '@/components/layout/Header.vue'
import PmTrack from '@/components/Track.vue'
import PmLoader from '@/components/shared/Loader.vue'
import PmNotification from '@/components/shared/Notification.vue'

export default {
  name: 'app',

  components: { PmFooter, PmHeader, PmTrack, PmLoader, PmNotification },

  data () {
    return {
      schQ: '',
      tracks : [],
      isLoading: false,
      selectedTrack: '',
      showNotification : false,
      showSucess: false
    }
  },
  methods: {
    search() {
      if(this.schQ == ''){return}
      this.isLoading = true
      trackService.search(this.schQ)
      .then(res => {
        this.showNotification = res.tracks.total === 0
        this.tracks = res.tracks.items
        this.isLoading = false
      })
    },
    setSelectedTrack(id){
      this.selectedTrack = id
    }
  },

  watch: {
      showNotification() {
        if (this.showNotification) {
          setTimeout(() => {
            this.showNotification = false
          }, 3000 )
        }
      }
  },

  computed: {
    total(){
      return `Encontradas ${this.tracks.length} rolas.`
    }
  }
}
</script>

<style lang="scss">
@import "~bulma/bulma.sass";

.btnS{
  margin-top: -2vh;
  position: absolute;
  right: 0px;
  align-items: right;
}

.rltC{
  margin-top: 12.3%;
}

.rslt{
  font-size: 14px;
  padding: 3px;
}

.is-active{
  border: 3px #23d160 solid;
}

</style>
