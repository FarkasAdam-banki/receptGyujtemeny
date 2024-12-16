<script setup>
import { ref, defineProps, watch } from 'vue';

const props = defineProps({
  recipes: Array
});

const sortedArray = ref([...props.recipes]);

const emit = defineEmits(['handle-change']);

const diff = ref("");
const searchText = ref("");
const sortOption = ref("0");

watch([diff, searchText, sortOption], () => {
  let filtered = [...props.recipes];
  if (diff.value !== "") {
    filtered = filtered.filter(elem => elem.diffuculty === diff.value);
  }
  
  if (searchText.value.trim() !== "") {
    filtered = filtered.filter(elem =>
      elem.name.toLowerCase().includes(searchText.value.trim().toLowerCase())
    );
  }

  if (sortOption.value === "1") {
    filtered.sort((a, b) => a.name.localeCompare(b.name));
  } else if (sortOption.value === "0") {
    filtered.sort((a, b) => a.cooktime - b.cooktime);
  }
  sortedArray.value = filtered;
 
  emit('handle-change', sortedArray.value);
  
});
</script>

<template>
  <section>
    <div class="row">
    
      <input class="form-control" type="text" placeholder="Keressen receptet..." v-model="searchText"  />

      
      <div class="col-3">
        <select class="form-select" aria-label="Minden nehézség" v-model="diff">
          <option value="">Minden nehézség</option>
          <option value="könnyű">könnyű</option>
          <option value="közepes">közepes</option>
          <option value="nehéz">nehéz</option>
        </select>
      </div>

     
      <div class="col-3">
        <select class="form-select" aria-label="Elkészítési idő szerint" v-model="sortOption">
          <option value="0">Elkészítési idő szerint</option>
          <option value="1">Név szerint</option>
        </select>
      </div>
    </div>


  </section>
</template>
<style scoped>
section {
  background-color: rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 20px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  align-items: center;
}

input.form-control {
  flex: 1;
  min-width: 200px;
  padding: 10px 15px;
  border-radius: 5px;
  border: 1px solid #ced4da;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s, box-shadow 0.3s;
}

input.form-control:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
  outline: none;
}

.select-container {
  display: flex;
  flex-direction: column;
}

select.form-select {
  width: 100%;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ced4da;
  background-color: #fff;
  box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: border-color 0.3s, box-shadow 0.3s;
}

select.form-select:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
  outline: none;
}

select.form-select option {
  padding: 5px;
}

section .row div {
  flex-grow: 1;
  min-width: 150px;
}


</style>

