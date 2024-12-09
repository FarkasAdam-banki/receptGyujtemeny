<script setup>
import { ref } from 'vue'
</script>

<template>
  <section>
    <div class="row">
      <input class="form-control custom-search" type="text" placeholder="Keressen receptet...">
      
      <div class="col-3">
        <select class="form-select" aria-label="Minden nehézség">
          <option selected>Minden nehézség</option>
          <option value="1">könnyű</option>
          <option value="2">közepes</option>
          <option value="3">nehéz</option>
        </select>
      </div>

      <div class="col-3">
        <select class="form-select" aria-label="Elkészítési idő szerint">
          <option selected>Elkészítési idő szerint</option>
          <option value="1">név szerint</option>
        </select>
      </div>
    </div>
  </section>
</template>

<style scoped>

.custom-search {
  width: 200px;  
} 
</style>
