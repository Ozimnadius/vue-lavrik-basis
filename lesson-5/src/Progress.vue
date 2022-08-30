<template>
  <div class="progress">
    <div class="progress-bar" v-bind:style="width">
    </div>
  </div>
</template>

<script>
export default {
  name: "Progress",
  props: {
    max: Number,
    val: Number
  },
  computed: {
    width() {
      return {
        width: `${this.val / this.max * 100}%`
      }
    }
  },
}
</script>
