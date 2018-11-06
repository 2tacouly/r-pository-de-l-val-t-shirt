<template>
  <div >
    <!-- <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    
    <body>
        <Header/>        
        <Sidebar></Sidebar>
        <Main></Main>
    </body>

  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import Header from '@/components/Header.vue'
import Sidebar from '@/components/Sidebar.vue'
import Main from '@/components/Main.vue'

export default {
//   name: 'home',
  components: {
    // HelloWorld,
    Header,
    Sidebar,
    Main
  }
}
</script>

<style scoped lang="scss">


body {
    position: relative;   
    min-width: 800px;
    margin: auto;
    min-height: 100px;
    max-height: auto;
    width: 70vw;
    
}
</style>