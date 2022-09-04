<template>
  <footer class="footer">
    <p>Make Your Burger &copy; 2022</p>
  </footer>
</template>

<script>
  export default {
    name: 'Footer'
  }
</script>

<style scoped>
  .footer {
    height: 200px;
    background-color: #222;
    border-top: 4px solid #fcba03;
    color: #fcba03;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
  }
</style>