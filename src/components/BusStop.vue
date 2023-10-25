<script setup>
import { toRefs } from 'vue'

// Use props to receive peopleWaiting from the parent
const props = defineProps(['peopleWaiting'])
const { peopleWaiting } = toRefs(props);

const setPeopleWaiting = (e) => {
  const updatedValue = parseInt(e.target.value);
  // Inform the parent of the change
  emit('update:peopleWaiting', updatedValue);
};

</script>

<template>
  <label for="peopleWaiting">People waiting</label>
  <input id="peopleWaiting" @change="setPeopleWaiting($event)"  placeholder="0" :value="peopleWaiting" type="number" min="0" max="50">
</template>


<style scoped></style>