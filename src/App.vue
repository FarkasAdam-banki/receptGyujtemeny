<script setup>
import { ref } from 'vue';
import kereses from './components/kereses.vue';
import recept from './components/recept.vue';
import card from './components/card.vue';
import { recipeData } from './data/recipes.js';
import hozzaad from './components/hozzaad.vue';

const sortedRecipes = ref([]);
const page = ref(0);
const info = ref(null);

const handleChanges = (updatedList) => {
  sortedRecipes.value = updatedList;
};

handleChanges(recipeData);


const switchToAddPage = () => {
  closeReceptDetails();
  page.value = 1;
  handleChanges(recipeData);
};
const switchToListPage = () => {
  page.value = 0;
};
const showRecipeInfo = (recept) => {
  handleChanges(recipeData);
  info.value = recept;
};
const closeReceptDetails = () => {
  info.value = null;
};
</script>

<template>
  <div class="container-fluid">
    <header>
      <nav class="navbar navbar-expand-lg bg-body-tertiary">
        <a class="navbar-brand" href="#">Receptkönyv</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a
                class="nav-link active"
                aria-current="page"
                href="#"
                @click="switchToListPage()"
                >Receptek</a
              >
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="switchToAddPage()">új recept</a>
            </li>
          </ul>
        </div>
      </nav>
    </header>
    <main>
      <div v-if="page == 0 && info == null">
        <kereses :recipes="recipeData" @handle-change="handleChanges" />

        <div class="row list">
          <div v-if="sortedRecipes.length>0" class="col-12 col-md-6 col-lg-4 mb-4"  v-for="recept in sortedRecipes"  :key="recept.id" >
            <card :recipe="recept" @recipe-info="showRecipeInfo" />
          </div>
          <div v-else>
              <p>nincs találat</p>
          </div>
        </div>
      </div>
      <div>
        <hozzaad v-if="page == 1" />
      </div>
      <div v-if="info">
        <recept :recipe="info" @close-details="closeReceptDetails" />
      </div>
    </main>
  </div>
</template>



<style scoped>

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
}

.list{
  padding: 0px 400px;
}
.navbar{
  background-color: rgba(0, 0, 0, 0.0) !important;
}
header {
  padding: 5px 50px;
  background-color: rgba(0, 0, 0, 0.3);
}

.navbar-nav, .nav-item, .nav-link {
  color: #ffffff !important;
  font-size: 1.2rem;
  padding: 5px 10px;
}

.list p {
  font-size: 1.7rem; 
  font-weight: bold; 
  color: #ff4141;
  text-align: center; 
  margin-top: 20px;
  background-color: #ffbebe; 
  padding: 10px 20px; 
  border-radius: 8px; 
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}


.navbar-brand {
  font-size: 1.5rem;
  color: #ffffff !important;
}


 .nav-item:hover {
  background-color: rgba(0, 0, 0, 0.3);
  border-radius: 5px;
}

main {
  padding: 30px;
}

.card {
  width: 100%;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  background-color: #fff;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
}

.card-body {
  padding: 15px;
}

input.form-control,
select.form-select {
  margin: 10px 0;
}
@media (max-width: 1900px) {
  .list{
    padding: 0px 200px;
  }
}

@media (max-width: 1750px) {
  .list{
    padding: 0px 100px;
  }
}
@media (max-width: 1500px) {
  .list{
    padding: 0px 50px;
  }
}
@media (max-width:950px) {
  .list{
    padding: 0px 20px;
  }
}
@media (max-width:500px) {
  .list{
    padding: 0px;
  }
  main{
    padding:10px 10px;
  }
}
@media (max-width:330px) {
  .navbar-brand{
    font-size: 20px;
    margin: 0px;
  }
}

</style>