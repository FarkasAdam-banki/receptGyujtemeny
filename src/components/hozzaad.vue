<script setup>
import { ref } from 'vue';
import { recipeData } from '../data/recipes.js';

const name = ref('');
const diffuculty = ref('');
const cooktime = ref(0);
const imageurl = ref(null);
const imagePreview = ref(null); 
const description = ref('');
const recipes = ref(recipeData);

const isModalVisible = ref(false);

const addRecipe = () => {
  if (!name.value.trim() || !diffuculty.value.trim() || !cooktime.value || !description.value.trim() || !imageurl.value) {
    alert('Kérlek, tölts ki minden mezőt, és ne csak szóközöket adj meg!');
    return;
  }

  const newId = String(recipes.value.length + 1); 
  const newRecipe = {
    id: newId,
    name: name.value,
    diffuculty: diffuculty.value,
    cooktime: cooktime.value,
    imageurl: imagePreview.value, 
    description: description.value,
  };

  recipes.value.push(newRecipe);


  isModalVisible.value = true;
  name.value = '';
  diffuculty.value = '';
  cooktime.value = 0;
  imageurl.value = null;
  imagePreview.value = null; 
  description.value = '';
};

const handleFileUpload = (e) => {
  const file = e.target.files[0];
  if (file) {
    imageurl.value = file;
    imagePreview.value = URL.createObjectURL(file); 
  } else {
    imageurl.value = null;
    imagePreview.value = null; 
  }
};

const closeModal = () => {
  isModalVisible.value = false;
};
</script>

<template>
  <section>
    <div class="row">
      <div class="col-12">
        <h3>Új recept hozzáadása</h3>
        <form @submit.prevent="addRecipe">
          <div class="mb-3">
            <label for="name" class="form-label">Recept neve</label>
            <input type="text" id="name" class="form-control" v-model="name" required maxlength="55"/>
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
            <input type="number" id="cooktime" class="form-control" v-model="cooktime" min="1" max="1000" required />
          </div>

          <div class="mb-3">
            <label for="imageurl" class="form-label">Recept képe</label>
            <input type="file" id="imageurl" class="form-control" @change="handleFileUpload" accept="image/*"  required/>
          </div>

          <div class="mb-3">
            <label for="description" class="form-label">Leírás</label>
            <textarea id="description" class="form-control"  maxlength="1000" v-model="description" rows="4" required></textarea>
          </div>

          <button type="submit" class="btn btn-primary">Recept hozzáadása</button>
        </form>
      </div>
    </div>
  </section>


  <div v-if="isModalVisible" class="modal fade show" tabindex="-1" style="display: block;">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Sikeres hozzáadás</h5>
          <button type="button" class="btn-close" @click="closeModal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <p>A recept sikeresen hozzáadásra került!</p>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" @click="closeModal">Bezárás</button>
        </div>
      </div>
    </div>
  </div>
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

.modal.fade {
  display: block;
  background-color: rgba(0, 0, 0, 0.5);
}
.modal-dialog {
  max-width: 400px;
  margin: 100px auto;
}
.modal-header {
  border-bottom: none;
}
.modal-body {
  text-align: center;
}
.modal-footer {
  border-top: none;
}


</style>
