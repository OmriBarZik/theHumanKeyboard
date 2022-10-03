<script setup>
import SingleLetter from './components/SingleLetter.vue';
// import { letters } from "./letters";
</script>

<script>
export default {
  data() {
    return {
      letters: '',
    };
  },
};
</script>

<template>
  <input type="text" v-model="letters" />
  {{ letters }}
  <hr />
  <SingleLetter :letters="letters"></SingleLetter>
  <!-- <SingleLetter
    v-for="letter in letters"
    v-bind:key="letter"
    :letter="letter"
  ></SingleLetter> -->
</template>
