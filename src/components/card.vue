<script setup>
import { defineEmits } from 'vue';
const props = defineProps({
    recipe : Object
})

const getURL = (url) =>{
    return new URL(url,import.meta.url).href
}

const emit = defineEmits(["recipe-info"])

const recpetReszlet = (recipe) =>{
emit('recipe-info',recipe)
}


</script>

<template>

    <main>
        
        <div class="recipes">
             <div class="card">
        <img class="card-img-top" :src="getURL(recipe.imageurl)" alt="Card image cap">
        <div class="card-body">
            <h5 class="card-title">{{ recipe.name }}</h5>
            <p class="card-text"><small class="text-body-secondary">Elkészitési idő: {{recipe.cooktime}} perc</small></p>
            <p 
            class="card-text diffuculty-text"
            :class="{  'bg-danger text-white': recipe.diffuculty === 'nehéz','bg-success text-white': recipe.diffuculty === 'könnyű','bg-warning text-dark': recipe.diffuculty === 'közepes' }"
          >
            {{ recipe.diffuculty }}
          </p>
          <p><a href="#" class="btn btn-primary" @click="recpetReszlet(recipe)">Részletek</a></p>
            
        </div>
        </div>
        </div>

    
    </main>
             
</template>

<style scoped>

.recipes {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  width: 300px;
  border: 1px solid #dee2e6;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s, box-shadow 0.3s;
  overflow: hidden;
  background-color: #fff;
  height:450px ;
}

.card:hover {
  transform: translateY(-5px);
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}

.card-img-top {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-bottom: 1px solid #dee2e6;
}

.card-body {
  padding: 15px;
  text-align: center;
}

.card-title {
  font-size: 1.2rem;
  font-weight: bold;
  margin-bottom: 10px;
  height: 70px
}

.card-text {
  margin-bottom: 20px;
}

.diffuculty-text {
  padding: 5px 10px;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: bold;
  text-transform: capitalize;
}

.bg-danger {
  background-color: #dc3545 !important;
}

.bg-warning {
  background-color: #ffc107 !important;
}

.bg-success {
  background-color: #28a745 !important;
}

.text-white {
  color: #fff !important;
}

.text-dark {
  color: #212529 !important;
}

.btn-primary {
  padding: 8px 12px;
  font-size: 0.9rem;
  border-radius: 20px;
  transition: background-color 0.3s, transform 0.3s;
}

.btn-primary:hover {
  background-color: #0056b3;
  transform: scale(1.05);
}
@media (max-width: 370px) {
  .recipes{
    padding: 20px 0px;
  }
}
</style>