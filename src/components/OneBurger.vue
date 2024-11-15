<template>
  <div class="burger">
    <h3>{{ burger.name }}</h3>
    <img v-bind:src="burger.url"/>
    <ul>

    </ul>
  </div>
</template>

<script>
export default {
  name: 'OneBurger',
  props: {
    burger: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.burger {
  display: inline-block;
  margin: 15px;
  vertical-align: top; /* Ensures proper alignment for differing heights */
  background-color: #da5d5dc3;
  padding: 16px;
  border-radius: 8px;
  text-align: center;
  color: #ff5500;
  height: 350px;
  width: calc((100%-6*8px)/3);
}


.burger img {
  width: 200px;
  height: auto;
}
</style>