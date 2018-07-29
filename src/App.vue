<template>
  <div id="app">
   <image-show :images="images"/> 
  </div>
</template>

<script>
import imageShow from './components/imageShow'

export default {
  name: 'App',
  components: {
    imageShow
  },
  data () {
    return {
      images: [
        {img: require('./assets/1.jpg')},
        {img: require('./assets/2.jpg')},
        {img: require('./assets/3.jpg')},
        {img: require('./assets/4.jpg')},
        {img: require('./assets/5.jpg')}
      ]
    }
  }
}
</script>

<style>

</style>
