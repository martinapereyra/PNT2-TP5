<template>
  <div>
    <Cabecera :colorDisplay="colorDisplay" :header="header"></Cabecera>
		<div id="navigator">
			<button @click="start()">{{startText}}</button>
			<span id="message"> {{messageDisplay}}</span>
			<button @click="easyPlay()" :class="easyClass" >easy</button>
			<button @click="hardPlay()" :class="hardClass" >hard</button>
		</div>
		<GrillaColores 
      :squares="squares" 
      :colorDisplay="colorDisplay" 
      @message-display="messageDisplay=$event"
      @restart-text="startText=$event"
      @header-background-color="header.backgroundColor=$event">
    </GrillaColores>
	</div>
</template>

<script>

import Cabecera from './Cabecera.vue'
import GrillaColores from './GrillaColores.vue'

  export default  {
    name: 'src-components-navegacion',
    components: {
      Cabecera,
      GrillaColores
    },
    data () {
      return {
        colorCount : 6,
        isHard : true,
        easyClass : '',
        hardClass : 'selected',
        colorMessage : '',
        startText : '',
        squares : [],
        colorDisplay : '',
        header : {
          backgroundColor : 'steelblue'
        },
        messageDisplay : '',
        colors : [],
      }
    },

    mounted () {
      this.startText = 'New Colors!'
      this.colors = this.createNewColors(this.colorCount)
      this.colorDisplay = this.colors[this.pickColor()]
      this.squares = this.inicializarSquares()
    },

    methods: {

       start(){
        this.startText = 'New Colors!'
        this.colors = this.createNewColors(this.colorCount)
        this.colorDisplay = this.colors[this.pickColor()]
        this.header.backgroundColor = 'steelblue'
        this.messageDisplay = ''
        for(let i = 0; i < this.squares.length ; i++){
          this.squares[i].backgroundColor = this.colors[i]
        }
      },

      easyPlay(){
        if(this.isHard){
          this.isHard = false;
          this.easyClass = 'selected'
          this.hardClass = ''
          this.colorCount = 3
          for(let i = 0 ; i < this.colorCount ; i++){
            this.squares[i + 3].display = 'none'
          }
          this.start()
        }
      },
      hardPlay(){
        if(!this.isHard){
          this.isHard = true;
          this.hardClass = 'selected'
          this.easyClass = ''
          this.colorCount = 6
          this.start()
          for(let i = 3 ; i < this.colorCount ; i++){
            this.squares[i].display = 'block'
          }
        }
      },
     
      pickColor() {
        let quantity;
        if (this.isHard) {
          quantity = 6;
        } else {
          quantity = 3;
        }
        return Math.floor(Math.random() * quantity);
      },

      createNewColors(numbers){
        let colors = []
        for (let i = 0 ; i < numbers ; i++){
          colors.push(this.createRandomStringColor())
        }
        return colors;
      },

      createRandomStringColor(){
        return "rgb(" + this.randomInt() + ", " + this.randomInt() + ", " + this.randomInt() + ")"
      },

      randomInt() {
        return Math.floor(Math.random() * 256)
      },

      inicializarSquares(){
        let newSquares = []
        for(let i = 0 ; i < this.colorCount ; i++){
          newSquares.push(
            { 
              backgroundColor : this.colors[i]
            }
          )
        }
        return newSquares
      },

    },
    
  }
</script>

<style scoped lang="css">
  #navigator {
    background: #ffffff;
    height: 30px;
    text-align: center;
    margin: 0;
    margin-top: -30px;
  }
  #message {
    color: #000000;
    display: inline-block;
    width: 20%;
  }
  .selected {
    background-color: steelblue;
    color: white;
  }
  button {
    border: none;
    background-color: white;
    font-family: "Montserrat", "Avenir";
    text-transform: uppercase;
    height: 100%;
    font-weight: 700;
    letter-spacing: 1px;
    color: steelblue;
    transition: all 0.3s;
    outline: none;
  }
  button:hover {
    color: white;
    background-color: steelblue;
  }
</style>