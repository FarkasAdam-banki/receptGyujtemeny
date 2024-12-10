<script setup>
import { ref, onMounted } from 'vue';
import kereses from './components/kereses.vue'
import card from './components/card.vue'
import {recipeData} from './data/recipes.js'


const szurtReceptek = ref([]);

const handleNehezsegValtozas = (updatedList) => {
  szurtReceptek.value = updatedList;
};

onMounted(() => {
  handleNehezsegValtozas(recipeData);
});

</script>

<template>
  <div class="container-fluid">
    <header>
                  
                    <nav class="navbar navbar-expand-lg bg-body-tertiary">
  
                  <a class="navbar-brand" href="#">Receptek</a>
                  <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
                     <span class="navbar-toggler-icon"></span>
                    </button>
                    <div class="collapse navbar-collapse" id="navbarNav">
                     <ul class="navbar-nav">
                     <li class="nav-item">
                     <a class="nav-link active" aria-current="page" href="#">Főoldal</a>
                     </li>
                     <li class="nav-item">
                     <a class="nav-link" href="#">Receptek</a>
                   </li>
                    <li class="nav-item">
                     <a class="nav-link" href="#">új recept</a>
                     </li>
                   <li class="nav-item">
          <a class="nav-link" href="#">kedvencek</a>
        </li>
      </ul>
    </div>
 
</nav>

    </header>  
    <main>
      <kereses :elemek="recipeData"  @nehezseg-valtozas="handleNehezsegValtozas"/>

      <div class="row lista">
        
        <div class="col-12 col-md-6 col-lg-4 mb-4" v-for="recept in szurtReceptek" :key="recept.id">
          <card :recept="recept" />
        </div>
      </div>

    </main>
    <footer>


    </footer>
  </div>
      

</template>


<style scoped>


</style>
