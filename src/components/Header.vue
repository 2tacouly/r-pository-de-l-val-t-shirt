<template>
  <div class="header entete">
    <header>
        <h1>Challenge – TeeShirtz</h1>
        <hr>
    </header>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

header {
    height: auto;
    margin: auto;
    width: 100%;
    max-width: 70vw;
    min-width: 800px;
    position: fixed;
}
div.entete {
    height: 100px;
}
hr {
    background: #42b983;
    height: 2px;
    width: 100%;
}
</style>
