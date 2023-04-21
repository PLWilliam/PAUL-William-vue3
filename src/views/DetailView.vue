<script setup>

import {onBeforeMount,ref} from 'vue'
import axios from 'axios'
import {useRoute} from 'vue-router'

const route = useRoute();

const getId = ref()
const amiibo = ref('')

const fetchOneAmiibo = async()=>{
    getId.value = route.params.id;
    const oneAmiibo = await axios.get('https://www.amiiboapi.com/api/amiibo/?tail='+getId.value)
    const {data,status} = oneAmiibo
    if(status == 200){
        amiibo.value = data.amiibo[0];
        // console.log(amiibo.value)
    }
    else{
        console.warn(status)
    }
}


onBeforeMount(async ()=>{
    await fetchOneAmiibo();
})

</script>

<template>
    <!-- Main -->
    <section id="main">
        <div class="container">
            <div class="row">
                <div class="col-4 col-12-medium">

                    <!-- Sidebar -->
                        <section class="box">
                            <header>
                                <h3>Infos</h3>
                            </header>
                            <p> amiiboSeries: <b>{{ amiibo.amiiboSeries }}</b> <br />
                                character: {{ amiibo.character }}<br />
                                gameSeries: {{ amiibo.gameSeries }}<br />
                                type: card
                            </p>
                            
                        </section>
                        <section class="box">
                            <header>
                                <h3>Dates sorties</h3>
                            </header>
                            
                            <ul class="divided">
                                <li v-for="(release,key) in amiibo.release"> {{ key }} : {{ release }}</li>
                            </ul>
                            
                        </section>

                </div>
                <div class="col-8 col-12-medium imp-medium">

                    <!-- Content -->
                        <article class="box post">
                            <a href="#" class="featured"><img :src="`${amiibo.image}`" alt="" /></a>
                            <header>
                                <h2>{{ amiibo.name }}</h2>
                                <p>{{ amiibo.type }}</p>
                            </header>
                        </article>

                </div>
            </div>
        </div>
    </section>
</template>
