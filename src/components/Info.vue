<template>
  <div>
    <h2>Раунд: {{ round }}</h2>
    <button @click="$emit('start')">Начать</button>
    <p v-if="lose">Извините, вы проиграли после {{ roundsPassed }} раундов!</p>
  </div>
</template>

<script>
export default {
  props: ['round', 'roundsPassed', 'lose']
}
</script>

<style lang="sass" scoped>

div
  margin-top: 90px

button
  width: 5em
  box-sizing: border-box
  font-size: 1.4em
  -webkit-border-radius: 10px 10px 10px 10px
  border-radius: 10px 10px 10px 10px
  background: #6DABE8
  border: none
  padding: 0.3em 0.6em

button:hover 
  background: #78BCFF

</style>