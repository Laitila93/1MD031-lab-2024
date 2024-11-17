<template>

<main>
            <header>
                <h1>Welcome to Bob's Burgers</h1>
            </header>
            <section id="burgers">
                <section>
                <h3>Select burger</h3>
                <h4>This is where you execute burger selection</h4>
                </section>
                <Burger v-for="burger in burgers"
            v-bind:burger="burger" 
            v-bind:key="burger.name"/>
            </section>
            <section>
                <h2>Customer information</h2>
                <h4>This is where you provide necessary information</h4>
            </section>
            <section>
                <h3>Delivery information:</h3>
            </section>
            <section id="contact">
                <form>
                    <p>
                        <label for="Full name">Name</label><br>
                        <input v-model="name" placeholder="Full name" />
                        <div>Name: {{name}}</div>
                    </p>
                    <p>
                        <label for="email">E-mail</label><br>
                        <input v-model="email" placeholder="E-mail adress" />
                    </p>
                    <p>
                        <label for="Street">Street</label><br>
                        <input v-model="street" placeholder="Street" />
                    </p>
                    <p>
                        <label for="House">House</label><br>
                        <input v-model="house" placeholder="House" />
                    </p>
                    <p>
                        <label for="payment option">Payment option</label><br>
                        <select v-model="selected">
                          <option disabled value="">Please select one</option>
                            <option>Bitcoin</option>
                            <option>Cash</option>
                            <option>Fish</option>
                            <option>Gold</option>
                            <option>Candy</option>
                        </select>
                     </p>
                     <section>
                      <h4>Select a gender:</h4>
                      <div>
                        <input type="radio" id="male" value="male" v-model="picked" name="gender" />
                        <label for="male">Male</label><br>

                        <input type="radio" id="female" value="female" v-model="picked" name="gender" />
                        <label for="female">Female</label><br>

                        <input type="radio" id="noPreference" value="Do not wish to provide" v-model="picked" name="gender" />
                        <label for="noPreference">Do not wish to provide</label><br>
                        <div>Picked: {{ picked }}</div>
                      </div>
                    </section>

                </form>

                <button type="submit">
                    <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTrvlSrN1N29iRIz_s9KkOE-_g5klfNJ_sIfQ&s" style="width: 200px">
                </button>
            </section>
            
        </main>
        <hr>
        <footer>
            &copy;2024 Burger.inc
        </footer>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io("localhost:3000");
function MenuItem() {
  this.name = "";
  this.image = "";
  this.kCal = "";
  this.gluten = false;
  this.lactose = false;

}
let myBurgers = [ 
  {name: "burger1", kCal: 300, gluten: true, lactose: false, image: "https://img.freepik.com/free-vector/realistic-burger-illustration_52683-153859.jpg?t=st=1730964219~exp=1730967819~hmac=3186965dab7f3a144a7c56119278acdb5296670ba9225f0fd6975fc1264ea285&w=826"},
  {name: "burger2", kCal: 200, gluten: false, lactose: true, image: "https://img.freepik.com/free-photo/tasty-hamburger-with-flying-ingredients-splash-sauce-dark-background_90220-1269.jpg?t=st=1730964269~exp=1730967869~hmac=c763a4d12a822b21a88b9fbd25be29be4c3d66953de328577ee41b817e69a851&w=826"},
  {name: "burger3", kCal: 400, gluten: true, lactose: true, image: "https://img.freepik.com/premium-photo/close-up-globe-burger-table-against-black-background_1048944-12365361.jpg?w=1060"}
  ,{name: "burger1", kCal: 300, gluten: true, lactose: false, image: "https://img.freepik.com/free-vector/realistic-burger-illustration_52683-153859.jpg?t=st=1730964219~exp=1730967819~hmac=3186965dab7f3a144a7c56119278acdb5296670ba9225f0fd6975fc1264ea285&w=826"},
  {name: "burger2", kCal: 200, gluten: false, lactose: true, image: "https://img.freepik.com/free-photo/tasty-hamburger-with-flying-ingredients-splash-sauce-dark-background_90220-1269.jpg?t=st=1730964269~exp=1730967869~hmac=c763a4d12a822b21a88b9fbd25be29be4c3d66953de328577ee41b817e69a851&w=826"},
  {name: "burger3", kCal: 400, gluten: true, lactose: true, image: "https://img.freepik.com/premium-photo/close-up-globe-burger-table-against-black-background_1048944-12365361.jpg?w=1060"}

]

export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers:menu
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }

  @import url('https://fonts.googleapis.com/css2?family=Agbalumo&family=Cormorant:wght@700&display=swap');
body {
    font-size: 12pt;
    font-family: Arial, sans-serif;
    color:black;
    background-color:powderblue;
}

section {
    margin: 5px 10px;
}
button {
    padding: 10px;
}
#burgers {
    background-color: black;
    color: white;
    border: 2px dotted white;
    margin: 5px
}

#contact {

    border: 2px dotted black;
}
button:hover {
    background-color: blue;
    cursor: pointer;
 }

p {

    color: red;
}
li  {
    font-weight: bold;
}

h1 {
    font-family: Arial, sans-serif;
    font-size: 36pt;
    padding-top: 50px;
}
main, header, footer, nav ul {
    max-width: 50rem;
    margin: 0 auto 0 auto;
    background-color: white;

}

/* nav ul li {
    display: inline-block;
    background-color: grey;
    padding: 1em;
    margin: 1em;
} */

header {
    color:black;
    background-image: url("../img/polacks.jpg");
    background-size: cover;
    overflow: hidden;
    width: 100%;
    height: 200px;
    opacity: 0.5;

}

header h1 {
    width:40rem;
    margin: 0 auto;
    text-align: center;
}

nav ul {
    display: grid;
    grid-template-columns: repeat(auto-fill, 9.25em);
    gap: 1em;
    padding: 0;
}

nav li {
    display: block;
    background-color: grey;
    padding: 1em;
}

.Very-good {
    color: green;
}

.Master {
    color: green;
    font-weight: bold;
}

.burger {
    color:#ff5500;
}



#idname {
    text-transform: uppercase;
}

.wrapper {
    display: grid;
    grid-gap: 10px;
    grid-template-columns: 33% 33% 33%;
}

.box {
    border-radius: 5px;
    padding: 20px;
}

.a {
    grid-column: 1;
}

.b {
    grid-column: 2;
}

.c {
    grid-column: 3;
}
</style>