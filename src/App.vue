<template lang="pug">
  #app
    img(src='./assets/logo.png')
    h1 Platzi Music
    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{ country.nombre }}
    <br>
    Spinner(v-show="loading")
    Artist(v-for="artist in artists" :key="artist.mbid" v-bind:artist="artist") {{ artist.name }}
</template>

<script>

  import Artist from './components/Artist.vue';
  import Spinner from './components/Spinner.vue';
  import getArtists from './api';

  export default {
    name: 'app',
    data () {
      return {
        artists: [],
        countries:  [
          {nombre: 'México', value: 'mexico'},
          {nombre: 'España', value: 'spain'},
          {nombre: 'Argentina', value: 'argentina'}
        ],
        selectedCountry: 'mexico',
        loading: true
      }
    },
    components: {
      Artist,
      Spinner
    },
    methods:{
      refreshArtists(){
        this.loading = true;
        this.artists = [];
        // Si usamos un arrow function a partir de ECMASCRIPT 6 el this toma el contexto automaticamente del exterior
        getArtists(this.selectedCountry).then(artists => {
          this.artists = artists;
          this.loading = false;
        });
        // Si usamos un callback 'function (...)' tenemos que usar un _this con el this del contexto exterior
        // let _this = this;
        // getArtists(this.selectedCountry).then(function(artists) { 
        //   _this.artists = artists;
        // });
      }
    },
    mounted: function(){
        this.refreshArtists();
    },
    watch: {
      selectedCountry: function() {
          this.refreshArtists();
      }
    }
  }
</script>

<style lang="stylus">
  #app
    font-family 'Avenir', Helvetica, Arial, sans-serif
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    text-align center
    color #2c3e50
    margin-top 60px

  h1, h2
    font-weight normal

  ul
    list-style-type none
    padding 0

  li
    display inline-block
    margin 0 10px

  a
    color #42b983
</style>