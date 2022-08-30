<template>
  <div class="item">
    <button class="btn btn-primary"
            v-on:click="showRes = !showRes">
      {{ btnTxt }}
    </button>
    <hr>
    <app-progress
      v-bind:val="sum"
      v-bind:max="maxItems * 5"
    ></app-progress>
    <br>
    <transition name="slide">
      <h2 class="alert alert-success"
          v-show="showRes">
        Your profit {{ sum }}
      </h2>
    </transition>
    <hr>
    <app-progress
      v-bind:val="numbers.length"
      v-bind:max="maxItems"></app-progress>
    <br>
    <button type="button" class="btn btn-success"
            v-on:click="addNumber"
            v-bind:disabled="done">
      Add number
    </button>
    <br>
    <br>
    <ul class="list-group">
      <li class="list-group-item"
          v-for="number in numbers">
        {{ number }}
      </li>
    </ul>
    <br>
    <button type="button" class="btn btn-danger"
            v-on:click="numbers=[]">
      Delete numbers
    </button>
  </div>
</template>

<script>
import Progress from "./Progress.vue";

export default {
  data() {
    return {
      showRes: true,
      numbers: [],
      maxItems: 10
    }
  },
  methods: {
    addNumber() {
      if (!this.done) {
        return this.numbers.push(Math.floor(Math.random() * 11) - 5);
      }
    }
  },
  computed: {
    sum() {
      return this.numbers.reduce((sum, num) => sum + num, 0);
    },
    btnTxt() {
      return this.showHeader ? 'Hide result' : 'Show result';
    },
    done() {
      return this.numbers.length >= this.maxItems;
    }
  },
  components:{
    AppProgress: Progress
  }
}
</script>

<style scoped>
.item {
  width: 100%;
  padding: 50px;
}

.slide-enter {
  opacity: 0;
}

.slide-enter-active {
  transition: opacity 0.5s;
}

.slide-leave-active {
  transition: opacity 0.5s;
}

.slide-leave-to {
  opacity: 0;
}
</style>
