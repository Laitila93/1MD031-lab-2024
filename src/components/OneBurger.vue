<template>
  <div class="burger">
    <h3>{{ burger.name }}</h3>
    <img v-bind:src="burger.url"/>
    <div>
      <ul>
        <li>{{ burger.kCal }}:kCal</li>
        <li v-if="burger.gluten">Contains gluten</li>
        <li v-if="burger.lactose">Contains lactose</li>
      </ul>
      <div>
        <button type="buttonRemove" v-on:click="removeBurger">-</button>
          {{ amountOrdered }}
        <button type="buttonAdd" v-on:click="addBurger">+</button>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OneBurger',
  gluten: false,
  lactose: false,
  props: {
    burger: Object
  },
  data: function () {
  return {
    amountOrdered: 0,
  }
},
methods: {
  addBurger() {
    this.amountOrdered += 1;
    this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              }
  );
  
  },
  removeBurger() {
    this.amountOrdered -= 1;
  }
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
  
  color: #ff5500;
  height: 400px;
  width: calc((100%-6*8px)/3);
}
.burger li {
  size: 14px;
  color: black;
}

.burger div div {
  text-align: center;
}


.burger img {
  width: 200px;
  height: auto;
}
</style>