<template>
  <div>
        <header class="front">
            <img src="https://www.nstgroup.co.uk/Admin/Public/GetImage.ashx?Image=/Files/Brand%20Images/Headers/nst/swiss-alps-plp-header-nst.jpg&Crop=0&Format=webp&Height=650&Compression=75&Quality=85&DoNotUpscale=True" id="bildfront">
            <h1 id="textfront">Välkommen till Skiburgers</h1>
        </header> 
        <main>
        <div id="Hamburgare">
          <h3> Vår meny </h3>
          <p> Välj en Hamburgare</p>
        
        <div class="wrapper">
          <Burger v-for="burger in burgers"
                  v-bind:burger="burger"
                  v-bind:key="burger.name"
                  v-on:orderedBurgers="addToOrder($event)"/>
        </div>
      </div>

        
            <section id="information">
                <h2>Kundinformation</h2>
                <div>
                    Fyll i lite information
                </div>
                <h4>Leveransinformation: </h4>
                <p>
                    <label for="Förnamn & efternamn">Ditt namn</label><br>
                    <input type="text" id="name" v-model="name" required="required" placeholder="Förnamn & efternamn">
                </p>
                <p>
                    <label for="Mailadress">E-mail</label><br>
                    <input type="email" id="email" v-model="em" placeholder="Mail">
                </p>
              <!----<p>
                    <label for="Adress">Adress</label><br>
                    <input type="text" id="adress" v-model="st" required="required" placeholder="Gatuadress">
                </p>
                <p>
                    <label for="Hus">Hus/Lägenhet</label><br>
                    <input type="number" id="number" v-model="numbr" required="required" placeholder="Hus-/Lägenhetsnummer">
                </p>--->

                <p>
                    <label for="Betalning">Betalningsalternativ</label><br>
                    <select id="Betalning" v-model="rcp">
                        <option>Swish</option>
                        <option>Kontant</option>
                        <option>Kort</option>
                        <option>Banköverföring</option>
                    </select>
                 </p>

                <p>
                    <label for="kon">Kön</label><br>
                    <input type="radio" id="Kvinna" v-model="kon" value="Kvinna" required="required">
                    <label for="Kvinna">Kvinna</label><br>
                    <input type="radio" id="Man" v-model="kon" value="Man" required="required">
                    <label for="Man">Man</label><br>
                    <input type="radio" id="Annat" v-model="kon" value="Icke-binär" required="required">
                    <label for="Annat">Icke-binär</label><br>
                    <input type="radio" id="Vill ej ange" v-model="kon" value="Vill ej ange" required="required">
                    <label for="Vill ej ange">Vill ej ange</label><br>
                </p>
                <button v-on:click="printOrder" type="submit">
                    <img src="data:image/png;base64,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" alt = "Span" style="width: 50px;">
                    Skicka beställning
                </button>
              </section>
            

              <div id="scroller">
                <div id="map" v-on:click="setLocation">
                  <div v-bind:style ="{left:location.x+'px', top:location.y+'px'}">
                      T
                    </div>
                    
                </div>
              </div>

        <footer>
            &#169 2022 Hamburgezas Inc.
        </footer>
      </main>

</div>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io();
//const menu = JSON.parse();

//function MenuItem(nm, url, kC, glu, lac) {
//this.name = nm;
//this.picture = url;
//this.kCal = kC;
//this.gluten = glu;
//this.lactose = lac;
//}

//const burger1 = new MenuItem("Störtloppsburgaren", "https://shared.cdn.smp.schibsted.com/v2/images/3fad8b85-50a4-4b4c-868d-ea07521b7f81?fit=crop&h=750&w=1000&s=8bf00cdb2c457330b3d88196c6fd605fa7ed89cc", "50", true, true)
//const burger2 = new MenuItem("Afterski", "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR410yU6QJ9JL64F1rl8aC5ZdWUxppQlLKNZQ&usqp=CAU", "50", true, false)
//const burger3 = new MenuItem("Toppburgaren", "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSVFlUPZw6QR4AKu9_VWgRyJax5l73OxX0rTQ&usqp=CAU", "50", false, false)

//const burger = [burger1, burger2, burger3];
//console.log(burger)
//console.log(menu)


export default {
  name: 'HomeView',
  components: {
    Burger
  
  },

  data: function () {
    return {
      burgers: menu,
      name:'',
      em:'',
      rcp:'',
      kon:'',
      orderedBurgers: {},
      location: {x:0, y:0}
    }
    namn: hejhej
    colorList: [{color: "#FF0000, lable:röd"},
                {color: "#FF0000, lable:röd"},
                {color: "#FF0000, lable:röd"},]
  },
  methods: {
     setSelectedBurgers: function(burgare){
      this.setSelectedBurgers.push(burger.name)
    },

    getSelectedBurger: function(event) {
      this.selectedBurger = event;
    },
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    checkDeliveryTime: function () {
      socket.emit
    },
    addOrder: function (event) {
      console.log(event);
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
                 this.location.x=event.clientX -10 - offset.x;
                 this.location.y=event.clientY -10 - offset.y;
    },
    printOrder: function () {
      console.log(this.name, this.em, this.rcp, this.kon);
      console.log(this.orderedBurgers);
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
        details: {
          x: this.location.x,
          y: this.location.y
        },
        orderItems: this.orderedBurgers,
        customerInformation:[this.name, this.em, this.rcp, this.kon]
      });
      
    },

    setLocation: function (event){
        this.location.x=event.clientX - 10 - event.currentTarget.getBoundingClientRect().left;
        this.location.y=event.clientY - 10 - event.currentTarget.getBoundingClientRect().top;
    },

    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
     
       
    }
  }
}
</script>

<style>
  #map {
    width:1920px;
    height: 1078px;
    background: url('/Users/victoriaberinder/Documents/gränssnitt/1md031-lab-2022/public/img/polacks.jpg');
    position: absolute;
    background-repeat: no-repeat;
    
}
#scroller {
  margin-left: 1.2em;
  width: 550px;
  height: 500px;
  overflow: scroll;
  position: relative;
  
}
body {
    font-family: 'Times New Roman', Times, serif;
    background-color: antiquewhite;
}

.textcolor {
    color: rgb(255, 116, 139);
    display: inline-block;
}
.front {
    overflow:hidden;
    margin: 15px 25px 25px 25px;
   
}
#bildfront {
    width: 100%;
    height: auto;
    opacity: 0.5;
      
}

#textfront {
    position: absolute;
    margin-top: -35%;
    margin-left: 15%;
    padding: 10%;
    -webkit-text-stroke: 1px black;
    font-family: sans; color: rgb(56, 129, 62);
}

.wrapper {
    display: grid;
    grid-gap: 1%;
    grid-template-columns: 33% 33% 33%;
}

.box {
    border-radius: 10px;
    padding: 10px;
    font-size: 100%;
}

#Hamburgare {
    background-color:rgb(183, 180, 180);
    color: black;
    margin: 15px 25px 25px 25px;
    border: 3px dashed antiquewhite;
    border-radius: 25px;
}

#bildburger {
    height: 150px;
    width: 90%;
}

#information {
    margin: 20px 0px;
    background-color: rgb(150, 185, 153);
    margin: 15px 25px 25px 25px;
    border: 3px dashed antiquewhite;
    border-radius: 25px;
}

button:hover {
    background-color: rebeccapurple;
    color: antiquewhite;
}

#knapp {
    cursor: pointer;
}

#map div {
    position: absolute;
    background: black;
    color: white;
    border-radius: 10px;
    width:20px;
    height:20px;
    text-align: center;
    
  }
</style>