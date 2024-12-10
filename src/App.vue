<script setup>
import { ref, onMounted } from 'vue';
import kereses from './components/kereses.vue'
import card from './components/card.vue'
import {recipeData} from './data/recipes.js'
import hozzaad from './components/hozzaad.vue';


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
      <div>
        <hozzaad />
      </div>

    </main>
    <footer>


    </footer>
  </div>
      

</template>



<style scoped>

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #f8f9fa;
  margin: 0;
  padding: 0;
}

.lista{
  padding: 0px 200px;
}
header {
  background-color: #f9f9f9;
  padding: 5px 50px;
}

.navbar {
  border-bottom: 2px solid #f9f9f9;
  background-color: #f9f9f9 !important;
}
.navbar-nav, .nav-item, .nav-link {
  color: #000000 !important;
  font-size: 1.1rem;
  padding: 5px 10px;
}


.navbar-brand {
  font-size: 1.5rem;
  color: #000000 !important;
}


 .nav-item:hover, .nav-link:hover {
  background-color: #a5a5a5;
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

@media (max-width: 1750px) {
  .lista{
    padding: 0px 100px;
  }
}
@media (max-width: 1500px) {
  .lista{
    padding: 0px 50px;
  }
}
@media (max-width:950px) {
  .lista{
    padding: 0px 20px;
  }
}
@media (max-width:500px) {
  .lista{
    padding: 0px;
  }
  main{
    padding:10px 10px;
  }
}


</style>

