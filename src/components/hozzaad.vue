<script setup>
import { ref } from 'vue';

const name = ref('');
const diffuculty = ref('');
const cooktime = ref(0);
const imageurl = ref('');
const description = ref('');

</script>

<template>
  <section>
    <div class="row">
      <div class="col-12">
        <h3>Új recept hozzáadása</h3>
        <form @submit.prevent="addRecipe">
          <div class="mb-3">
            <label for="name" class="form-label">Recept neve</label>
            <input type="text" id="name" class="form-control" v-model="name" required />
          </div>

          <div class="mb-3">
            <label for="diffuculty" class="form-label">Nehézség</label>
            <select id="diffuculty" class="form-select" v-model="diffuculty" required>
              <option value="">Válassz nehézséget</option>
              <option value="könnyű">Könnyű</option>
              <option value="közepes">Közepes</option>
              <option value="nehéz">Nehéz</option>
            </select>
          </div>

          <div class="mb-3">
            <label for="cooktime" class="form-label">Elkészítési idő (perc)</label>
            <input type="number" id="cooktime" class="form-control" v-model="cooktime" min="1" required />
          </div>

          <div class="mb-3">
            <label for="imageurl" class="form-label">Recept képe</label>
          </div>

          <div class="mb-3">
            <label for="description" class="form-label">Leírás</label>
            <textarea id="description" class="form-control" v-model="description" rows="4" required></textarea>
          </div>

          <button type="submit" class="btn btn-primary">Recept hozzáadása</button>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
section {
  background-color: #f9f9f9;
  border-radius: 8px;
  padding: 30px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  margin-top: 30px;
}

h3 {
  font-size: 1.5rem;
  margin-bottom: 20px;
}

.form-control, .form-select {
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ced4da;
  margin-bottom: 15px;
}

.btn-primary {
  padding: 10px 15px;
  font-size: 1rem;
  border-radius: 5px;
  transition: background-color 0.3s, transform 0.3s;
}

.btn-primary:hover {
  background-color: #0056b3;
  transform: scale(1.05);
}
</style>
