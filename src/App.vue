<template>
  <weather />
  <Comment />
    <Footer/>
</template>

<script>
import Weather from './components/Weather.vue'
import Comment from './components/Comment.vue'
import Footer from './components/Footer.vue'


export default {
  name: 'App',
  components: {
    Weather,
    Comment,
    Footer
    
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  line-height: 1.5em;
}
body{
  margin: 0;
  background: url("./assets/pexels-ben-mack-5707718.jpg");
  background-repeat: repeat-y;
}
#app{
    min-height: 100vh; 
    margin: 0; 
    display: grid;
    grid-template-rows: 1fr auto;
}

</style>
