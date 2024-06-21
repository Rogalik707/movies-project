<script lang="ts" setup>
import {defineProps, ref} from "vue";

const props = defineProps({
  name: String,
  namesArray: {
    type: Array,
    default: () => [],
  },
})
const isSelected = ref(false)
const emit = defineEmits(['update'])
const handleClick = (name: string) => {
  props.namesArray.find(item => item === name) ?
    isSelected.value = false : props.namesArray.length < 3 ?
      isSelected.value = true : isSelected.value = false;
  emit('update', name);
}
</script>

<template>
  <div
    :class="{'card': !isSelected, 'cardActive': isSelected }"
    @click="handleClick(<string>props.name)"
  >
    <h5 class="card-title">{{ name }}</h5>
  </div>
</template>

<style scoped>
.card {
  background-color: #3868f3;
  width: 100%;
  aspect-ratio: 1/1;
  border-radius: 10%;
  box-shadow: 0 0 100px #3868f3;
  transition: all 0.2s;
  user-select: none;


  &:hover {
    cursor: pointer;
    transform: scale(1.1);
    background-color: #ff98bd;
    box-shadow: 0 0 100px #ff98bd;
  }

  &:active {
    transform: scale(0.9);
  }
}

.cardActive {
  background-color: #f33879;
  box-shadow: 0 0 100px #f33879;
  width: 100%;
  aspect-ratio: 1/1;
  border-radius: 10%;
  transition: all 0.2s;
  user-select: none;


  &:hover {
    cursor: pointer;
    transform: scale(1.1);
  //background-color: #97b2fd; //box-shadow: 0 0 100px #97b2fd;
  }

  &:active {
    transform: scale(0.9);
  }
}

.card-title {
  margin: 7px;
}
</style>
