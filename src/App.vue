<template>
  <nav class="navbar bg-some-gray">
    <div class="container">
      <a class="navbar-brand text-white" @click="handleClick()">
        <img src="@/assets/tree.png" width="25" />
        <span class="mx-2">Árbol Genealógico</span>
      </a>
      <button class="btn btn-outline-light" @click="handleClick()">
        Volver
      </button>
    </div>
  </nav>
  <div class="bg-some-gray">
    <FamilyChart :key="key" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import FamilyChart from "@/components/FamilyChart.vue";

const key = ref(0);

const handleClick = () => {
  key.value = Math.random();
};
</script>

<style>
.bg-some-gray {
  background-color: #3b5560;
}
</style>
