<template>
  <h1>Flips {{ turnCount }}</h1>
  <div class="board">
    <Card v-for="(card, index) in cards" :key="index" :value="card.value" :selected="card.selected" :cardImage="card.cardImage" @click="FlipCard(index)"/>
  </div>


</template>

<script>
import Card from './components/Card.vue';

export default {
  name: 'App',
  components: {
    Card
  },

  data() {
    var turnCount = 0;
    const compareTwoCards =  []
    var isSelectable = true;
    var cards = [
      {value: 0, selected: false, cardImage: "VanYou"},
      {value: 0, selected: false, cardImage: "VanYou"},
      {value: 1, selected: false, cardImage: "FullParty"},
      {value: 1, selected: false, cardImage: "FullParty"},
      {value: 2, selected: false, cardImage: "VanSit"},
      {value: 2, selected: false, cardImage: "VanSit"},
      {value: 3, selected: false, cardImage: "Mmm"},
      {value: 3, selected: false, cardImage: "Mmm"},
      {value: 4, selected: false, cardImage: "Ricardo"},
      {value: 4, selected: false, cardImage: "Ricardo"},
      {value: 5, selected: false, cardImage: "BillyHat"},
      {value: 5, selected: false, cardImage: "BillyHat"},
      {value: 6, selected: false, cardImage: "SorryForWhat"},
      {value: 6, selected: false, cardImage: "SorryForWhat"},
      {value: 7, selected: false, cardImage: "threehundredbucks"},
      {value: 7, selected: false, cardImage: "threehundredbucks"},
      ];
    const numberOfPairs = 8;
    const cardImages = ['Van', 'FullParty']

    // for (let i = 1; i < numberOfPairs*2 + 1; i++) {
    //   const num = i;
    //   if(num%2 == 0){
    //     num = i / 2
    //   }else{
    //     num = i / 2 + 0.5
    //   }
    //   cards.push({value: num, selected: false, cardImage: cardImages[0]});
    //   console.log(cards[0]);
    // }

    cards = cards.sort(() => Math.random() - 0.5);

    return {cards, compareTwoCards, cardImages, isSelectable, turnCount};
  },

  methods: {
    FlipCard(index) {
      if(this.cards[index].selected == true){
        return;
      }
      if(!this.isSelectable){
        return;
      }

      if(this.compareTwoCards.length < 2){
        this.cards[index].selected = true;
        this.compareTwoCards.push(this.cards[index]);
        this.turnCount++;
      }
      if(this.compareTwoCards.length == 2){
        this.SimilarityCheck();
        this.isSelectable = false;
        //this.turnCount++;
      }

      //check if player wins
    },
    SimilarityCheck(){
      if(this.compareTwoCards[0].value == this.compareTwoCards[1].value){
        setTimeout(() => this.RemoveMathingCards(), 3000);
      }
      else {
        setTimeout(() => this.FlipCardsBackwards(), 2000);
      }
      
    },
    FlipCardsBackwards() {
      for (let i = 0; i < this.compareTwoCards.length; i++) {
        this.compareTwoCards[i].selected = false;
      }
      this.compareTwoCards = [];
      this.isSelectable = true;
    },

    //
    RemoveMathingCards() {
        var fel = this.cards.indexOf(this.compareTwoCards[0]);
        //this.cards.splice(fel, 1)
        this.cards[fel].selected = true;
        var sel = this.cards.indexOf(this.compareTwoCards[1]);
        //this.cards.splice(sel, 1)
        this.cards[sel].selected = true;
        this.compareTwoCards = [];
        this.isSelectable = true;

        //win condition
        for (let i = 0; i < 16; i++) {
          if(this.cards[i].selected == false){
            return;
          }
          //restart the game
          if(i == 15){
            if(confirm("You won in " + this.turnCount + " moves! Do you want to start over?")){
              location.reload();
            }
          }
        }
    },

  }


}

</script>

<style>
  html, body{
    margin: 0;
    padding: 0;
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    background-image: url('/images/OhShit.png');
    width: 100%;
    height: 100vh;

  }

  .board{
    display: grid;
    grid-template-columns: repeat(4, 200px);
    grid-template-rows: repeat(4, 200px);
    grid-column-gap: 50px;
    grid-row-gap: 50px;
    justify-content: center;
    padding-top: 5%;

  }

  h1 {
    font-size: 50px;
    color: white;
    text-align: center;
    margin: 0;
  }
</style>
