<script setup>
const props = defineProps({
  recipe: Object,
});

const emit = defineEmits(['close-details']);

const getURL = (url) => {
  return new URL(url, import.meta.url).href;
};


const closeDetails = () => {
  const detailsView = document.querySelector('.details-view');
  if (detailsView) {
    detailsView.classList.add('fade-out'); 
    setTimeout(() => {
      emit('close-details'); 
    }, 400); 
  }
};
</script>

<template>
    <main>
    <div class="details-view" v-show="recipe" :class="{'fade-in': showDetails}">
      <button class="close-btn" @click="closeDetails">X</button>
      
      
      <div class="details-card card">
        <img class="card-img-top" :src="getURL(recipe.imageurl)" alt="Card image cap">
        <div class="card-body">
          <h5 class="card-title">{{ recipe.name }}</h5>
          <p class="card-text"><small class="text-body-secondary">Elkészítési idő: {{ recipe.cooktime }} perc</small></p>
          <p class="card-text diffuculty-text" :class="{
            'bg-danger text-white': recipe.diffuculty === 'nehéz',
            'bg-success text-white': recipe.diffuculty === 'könnyű',
            'bg-warning text-dark': recipe.diffuculty === 'közepes'
          }">
            {{ recipe.diffuculty }}
          </p>
        </div>
      </div>
      <div class="details-description">
        <h3>Recept leírása</h3>
        <p>{{ recipe.description }}</p>
      </div>
    </div>
  </main>
</template>

<style scoped>
.details-view {
  display: flex;
  gap: 20px;
  padding: 20px;
  animation: slideInScale 0.6s ease forwards;
  position: relative;
  flex-wrap: wrap; 
  background-color: #eeeeee; 
  border-radius: 10px;
}

@keyframes slideInScale {
  0% {
    opacity: 0;
    transform: translateY(50px) scale(0.8);
  }
  60% {
    opacity: 1;
    transform: translateY(-5px) scale(1.03);
  }
  100% {
    transform: translateY(0) scale(1);
  }
}

@keyframes fadeOutScale {
  0% {
    opacity: 1;
    transform: scale(1);
  }
  100% {
    opacity: 0;
    transform: scale(0.8);
  }
}

.details-view.fade-out {
  animation: fadeOutScale 0.4s ease forwards;
}

.details-view.fade-in {
  animation: slideInScale 0.6s ease forwards;
}
.diffuculty-text {
  padding: 8px 12px;
  border-radius: 25px;
  font-size: 1rem;
  font-weight: bold;
  text-transform: capitalize;
  text-align: center; 
  margin-top: 10px;
}

.close-btn {
  position: absolute;
  top: 0px;
  right: 0px;
border: 1px solid #dcdcdc;
  background: #ff5f5f;
  color: white;
  font-size: 1.2rem;
  padding: 5px 10px;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.2s ease;
  width: 40px;
  height: 40px;
}

.close-btn:hover {
  background: #ff3b3b;
  transform: scale(1.1);
}

.details-card {
  flex: 1;
  max-width: 50%;
  background-color: #ffffff; 
  border-radius: 15px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.15); 
  overflow: hidden;
  border: 1px solid #e0e0e0; 
}
.card-body{
    text-align: center;
}

.details-card img {
  width: 100%;
  height: auto;
  max-height: 600px;
}

.details-description {
    height: fit-content;
    margin: auto 0px;
  flex: 1;
  font-size: 1.1rem; 
  line-height: 1.6; 
  overflow-y: auto; 
  background: #ffffff;
  border: 1px solid #dcdcdc; 
  padding: 30px 40px;
  background-color: #f4f4f9; 
  border-radius: 12px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.1);
}

.details-description h3 {
  font-size: 2rem; 
  font-weight: 600; 
  color: #333333; 
  margin-bottom: 15px;
  text-align: center;
  font-family: 'Playfair Display', serif; 
  letter-spacing: 1px; 
  text-transform: capitalize;
}


.details-description p {
  font-size: 18px;
  text-align: justify;
  color: #444444;
}

.details-description p::first-letter {
  font-size: 1.7rem; 
  font-weight: bold;
  color: #a37450; 
  padding-right: 2px;
  font-family: 'Playfair Display', serif; 
  text-transform: capitalize;
}

.details-description img {
  max-width: 100%; 
  border-radius: 5px; 
  margin-bottom: 20px; 
}

@media (max-width: 768px) {
  .details-view {
    flex-direction: column; 
    gap: 10px;
  }

  .details-card {
    max-width: 100%; 
  }

  .details-description {
    padding: 15px; 
  }

  .close-btn {
    font-size: 1rem; 
    padding: 5px 8px;
    z-index: 2;
  }

  .details-card img {
    max-height: 400px; 
  }
}

@media (max-width: 480px) {
  .close-btn {
    font-size: 0.9rem; 
    padding: 4px 7px;
  }
}

</style>
