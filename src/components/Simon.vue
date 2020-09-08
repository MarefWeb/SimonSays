<template>
  <div>
    <div class="simon">
      <ul>
        <li class="tile red" :class="{ 'lit': buttons[1].isActive, 'hoverable': interectiveMode }" @mousedown="$emit('mouse-down', 1)" @mouseup="$emit('mouse-up', 1)"></li>
        <li class="tile blue" :class="{ 'lit': buttons[2].isActive, 'hoverable': interectiveMode }" @mousedown="$emit('mouse-down', 2)" @mouseup="$emit('mouse-up', 2)"></li>
        <li class="tile yellow" :class="{ 'lit': buttons[3].isActive, 'hoverable': interectiveMode }" @mousedown="$emit('mouse-down', 3)" @mouseup="$emit('mouse-up', 3)"></li>
        <li class="tile green" :class="{ 'lit': buttons[4].isActive, 'hoverable': interectiveMode }" @mousedown="$emit('mouse-down', 4)" @mouseup="$emit('mouse-up', 4)"></li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
	props: ['buttons', 'interectiveMode']
}
</script>

<style lang="sass" scoped>

.simon
  background: #fff
  position: relative
  float: left
  margin-right: 3em
  width: 302px
  height: 295px
  -webkit-border-radius: 150px 150px 150px 150px
  border-radius: 150px 150px 150px 150px
  -moz-box-shadow: 2px 1px 12px #aaa
  -webkit-box-shadow: 2px 1px 12px #aaa
  -o-box-shadow: 2px 1px 12px #aaa
  box-shadow: 2px 1px 12px #aaa

.tile
	opacity: 0.6
	-webkit-transition: opacity 250ms ease
	-moz-transition: opacity 250ms ease
	-ms-transition: opacity 250ms ease
	-o-transition: opacity 250ms ease
	transition: opacity 250ms ease

.tile.lit
	opacity: 1

.red, .blue, .yellow, .green
	height: 290px
	-webkit-border-radius: 150px 150px 150px 150px
	border-radius: 150px 150px 150px 150px
	position: absolute
	text-indent: 10000px

.red:hover, .blue:hover, .yellow:hover, .green:hover
	border: 2px solid black

.red
	background: #FF5643
	clip: rect(0px, 300px, 150px, 150px)
	width: 296px

.blue
	background: dodgerblue
	clip: rect(0px, 150px, 150px, 0px)
	width: 300px

.yellow
	background: #FEEF33
	clip: rect(150px, 150px, 300px, 0px)
	width: 300px

.green
	background: #BEDE15
	clip: rect(150px,300px, 300px, 150px)
	width: 296px

</style>