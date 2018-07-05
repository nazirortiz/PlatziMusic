<template lang="pug">
  li
    h5: a(v-bind:href="artist.url" target="_blank") {{ artist.name }}
    img(:src="artist.image[1]['#text']" :alt="artist.name")
</template>

<script>
    export default {
        name: 'Artist',
        props: ['artist']
    }
</script>

<style lang="stylus" scoped>
  li
    margin 10px
</style>