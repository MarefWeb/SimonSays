<template>
  <div>
    <h2>Режимы игры:</h2>

    <input type="radio" name="mode" value="easy" id="easy" v-model.trim="mode" @change="send">
    <label for="easy">Легкий</label>
    <br>

    <input type="radio" name="mode" value="normal" id="normal" v-model.trim="mode" @change="send">
    <label for="normal">Средний</label>
    <br>

    <input type="radio" name="mode" value="hard" id="hard" v-model.trim="mode" @change="send">
    <label for="hard">Сложный</label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mode: 'easy'
    }
  },

  created() {
    this.$emit('changed-mode', this.mode)
  },

  methods: {
    send() {
      this.$emit('changed-mode', this.mode)
    }
  }
}
</script>

<style lang="sass" scoped>

h2
	margin-top: 30px
	margin-bottom: 5px

input
	margin-right: 10px

</style>