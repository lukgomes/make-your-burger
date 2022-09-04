<template>
  <div id="main-banner">
    <h1>Make your burger</h1>
  </div>
</template>

<script>
  export default {
    name: 'Banner'
  }
</script>

<style scoped>
  #main-banner {
    background-image: url(../../public/img/burger.jpg);
    /* background-image: url(/img/burger.jpg); */
    background-position: 0 -250px;
    background-size: cover;
    width: 100%;
    height: 500px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
  }

  #main-banner h1 {
    color: white;
    text-align: center;
    font-size: 60px;
    background-color: #222;
    padding: 20px 40px;
    border-radius: 10px;
    border-bottom: 4px solid #fcba0366;
    border-right: 4px solid #fcba03bb;
  }
</style>