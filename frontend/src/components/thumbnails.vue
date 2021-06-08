<!--
  - Copyright (c) 2018 LI Zhennan
  -
  - Use of this work is governed by an MIT License.
  - You may find a license copy in project root.
  -
  -->

<template>
  <div class="thumbnails">
    <h2>{{ $t("animal_code_title") }}</h2>
    <div class="animal" v-for="(pic, index) in animals" :key="index">
      <img @click="picClick(index)" :src="pic" alt="0" />{{index}}
    </div>
  </div>
</template>

<script>
import bus from "@/bus";
export default {
  name: "thumbnails",
  data() {
    return {};
  },
  methods: {
    picClick(index) {
      bus.$emit('animal', index)
    }
  },
  computed: {
    animals() {
      let animals = [];

      for (let i = 0; i <= 40; i++) {
        animals.push(require(`@/assets/thumbnails/${i}.tif.gif`));
      }
      return animals;
    },
  },
};
</script>

<style scoped>
img {
  width: 120px;
}

.animal {
  width: 120px;
  display: inline-block;
  font-size: 1.2em;
  margin: 40px 22px;
}

.thumbnails {
  max-width: 92%;
  margin: 50px 0 0 0;
}
</style>