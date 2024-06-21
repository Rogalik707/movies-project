<script setup lang="ts">
import GenreCard from "/src/components/genre-card.vue";
import {dataGenres} from "/src/local/localData";
import {ref, watch} from 'vue';

let namesArray = ref([]);
const handleAddName = (name: string) => {
  if (!namesArray.value.includes(name) && namesArray.value.length < 3) {
    namesArray.value = [...namesArray.value, name];
  } else {
    namesArray.value = namesArray.value.filter((item: string) => item !== name);
  }
};

watch(namesArray, (newVal: any) => {
  console.log('val', newVal);
})
</script>

<template>
  <div class="bg">
    <div class="title">
      <h2>Choose your favorite genre</h2>
    </div>
    <h4>{{ `${namesArray.length} / 3` }}</h4>
    <div class="bg-choosing-genre"></div>
    <div class="bg-circle-blue"></div>
    <div class="cards-list">
      <GenreCard
        @update="handleAddName(card.name)"
        v-for="card in dataGenres"
        :key="card.id"
        :name="card.name"
        :namesArray="namesArray"
      />
    </div>
    <div
      v-if="namesArray.length === 3"
      class="btn-wrapper"
    >
      <v-btn class="btn" color="#FFFFFF">
        Accept
      </v-btn>
    </div>
  </div>
</template>


<style scoped>
.bg-choosing-genre {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 900px;
  height: 100px;
  background-color: #eaeaea;
  border-radius: 50%;
  box-shadow: 0 0 500px #eaeaea;
  filter: blur(300px);
  z-index: -4;
}

.title {
  padding-top: 40px;
}

.cards-list {
  width: 30%;
  display: grid;
  margin: 50px auto 0 auto;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 1fr);
  gap: 15px;
  z-index: 10;
}

.btn-wrapper {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
}

.btn {
}
</style>
