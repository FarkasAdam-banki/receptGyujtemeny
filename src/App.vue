<script setup>
import Kereses from './components/kereses.vue';


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
   <kereses />               
</template>

<style scoped>
.navbar{
    padding: 20px;
}

</style>
