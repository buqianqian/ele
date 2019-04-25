<template>
  <div class="star" :class="starType">
    <span v-for="(itemClass,index) in itemClasses" :class="itemClass"></span>
  </div>
</template>

<script>
export default {
  props: {
    size: {
      type: Number
    },
    score: {
      type: Number
    }
  },
  computed: {
    starType () {
      return 'star-' + this.size
    }
  },
  created () {
    console.log(this.size)
  }
}
</script>

<style>

</style>
