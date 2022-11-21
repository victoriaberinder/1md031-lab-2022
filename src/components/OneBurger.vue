<template>
    <div id="Hamburgers">
        <h4>{{burger.name}}</h4>
        <button v-on:click=increase type="button">
          +
        </button>
        <button v-on:click=decrease type="button">
          -
        </button>
        <h5>Antal beställda: {{amountOrdered}}</h5>
        
        
        <img id="bildburger" v-bind:src="burger.picture">
        <ul>
            
            <li v-if="burger.name=='Störtloppsburgaren'">Alpost, picklad rödlök & vitlökssås</li>
            <li v-if="burger.name=='Störtloppsburgaren'">Serveras med en cola</li>
            <li v-if="burger.name=='Afterski'">Friterad kyckling, sallad & barbequesås </li>
            <li v-if="burger.name=='Afterski'">Serveras med valfri shot</li>
            <li v-if="burger.name=='Toppburgaren'">Oumph, tzatsiki & picklad vitkål</li>
            <li v-if="burger.name=='Toppburgaren'">Serveras med en kall öl</li>
            <li>{{burger.kCal}} kCal</li>
            <li v-if="burger.gluten">Innehåller <div class="textcolor">gluten</div></li>
            <li v-if="burger.lactose">Innehåller <div class="textcolor">laktos</div></li>
        </ul>
        
    </div>
</template>
  
  <script>
  export default {
    name: 'OneBurger',
    props: {
      burger: Object
    },
    data: function (){
      return {
        amountOrdered: 0,
      }
    },
    
    methods: {
      increase: function () {
      this.amountOrdered += 1
      this.$emit('orderedBurgers', {name: this.burger.name,
                                  amount: this.amountOrdered
                                  });
      
      },
      decrease: function() {
        if(this.amountOrdered >= 1){this.amountOrdered -=1}
        this.$emit('orderedBurgers', {name: this.burger.name,
                                  amount: this.amountOrdered
                                  });
        
      }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  
  .textcolor {
    color: rgb(56, 129, 62);;
    display: inline-block;
    text-transform: bold;
}
  .wrapper {
    display: none;
    grid-gap: 1%;
    grid-template-columns: 33% 33% 33%;
}

.box {
    border-radius: 10px;
    padding: 10px;
    font-size: 100%;
}

#bildburger {
    height: 150px;
    width: 90%;
}
#Hamburgare {
    background-color:rgb(157, 200, 212);
    color: antiquewhite;
    margin: 15px 25px 25px 25px;
    border: 3px solid black;
    border-radius: 25px;
}

#Hamburgers {
    background-color:rgb(183, 180, 180);
    color: black;
    margin: 15px 25px 25px 25px;
  
}
  </style>
  