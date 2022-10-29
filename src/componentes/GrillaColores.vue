<template>
  <div id="src-components-grillaColores">
		<div v-for="(square, index) in squares" :key="index">
      <div class="square" :style="square" @click='colorCheck(square)'></div>
    </div>
  </div>
</template>

<script>
  export default  {
    name: 'src-components-grillaColores',
    props: ['squares', 'colorDisplay'],
    data(){
      return{
        txtCorrect : 'You Picked Right!',
        txtAgain: 'Play Again!',
        txtTry: 'Try Again!'
      }
    },
    methods: {
      colorCheck(square){
        if(square.backgroundColor === this.colorDisplay){
          this.$emit('message-display', this.txtCorrect)
          this.setAllColorsTo(square.backgroundColor)
          this.$emit('restart-text', this.txtAgain )
          this.$emit('header-background-color', square.backgroundColor)
        }else{
          square.backgroundColor = 'transparent'
          this.$emit('message-display', this.txtTry )
        }
      },
      setAllColorsTo(color){
        this.squares.forEach( square => square.backgroundColor = color)
      }
    }
  }
</script>

<style scoped lang="css">

#src-components-grillaColores {
	margin: 20px auto;
	max-width: 600px;
}
.square {
	width: 30%;
	background: blue;
	padding-bottom: 30%;
	float: left;
	margin: 1.66%;
	border-radius: 10%;
	transition: background 0.8s;
	-webkit-transition: background 0.8s;
	-moz-transition: background 0.8s;
}

</style>