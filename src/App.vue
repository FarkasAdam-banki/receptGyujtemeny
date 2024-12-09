<script setup>
import Kereses from './components/kereses.vue';
import { recipeData } from './data/recipes';

const getURL = (url) =>{
    return new URL(url,import.meta.url).href
}

</script>

<template>
    <header>
                    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
                    <a class="navbar-brand" href="#">Logo</a>
                    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>
                    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                        <div class="navbar-nav">
                        <a class="nav-item nav-link active" href="#">Főoldal</a>
                        <a class="nav-item nav-link" href="#">Receptek</a>
                        <a class="nav-item nav-link" href="#">új recept</a>
                        <a class="nav-item nav-link" href="#">kedvencek</a>
                        </div>
                    </div>
                    </nav>

    </header>  


    <main>
        <div>
            <kereses />    
        </div>
        <div class="receptek">
             <div class="card" style="width: 18rem;" v-for="recept in recipeData">
        <img class="card-img-top" :src="getURL(recept.imageurl)" alt="Card image cap">
        <div class="card-body">
            <h5 class="card-title">{{ recept.name }}</h5>
            <p class="card-text">Some quick example text to build on the card title and make up the bulk of the card's content.</p>
            <a href="#" class="btn btn-primary">Go somewhere</a>
        </div>
        </div>
        </div>

               






    </main>

    <footer>



    </footer>


             
</template>

<style scoped>
.navbar{
    padding: 20px;
}

</style>
