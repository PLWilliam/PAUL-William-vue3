<script setup>

import { onBeforeMount,ref } from 'vue';
import {useRouter} from 'vue-router'
import axios from 'axios';

const router = useRouter();
const allAmiibo = ref();
const randomAmiiboList = ref([]);

const pageList = () =>{
    router.push({name:'list'})
}

const pageDetail =(id) =>{
    router.push({name:'detail',params:{id}})
}

const fetchAllAmiibo = async()=>{
    const amiibos = await axios.get('https://www.amiiboapi.com/api/amiibo/')
    const {data,status} = amiibos
    if(status == 200){
        allAmiibo.value = data.amiibo;
    }
    else{
        console.warn(status)
    }
}

const getRandomAmiibo = async() => {
    const numberAmiibo = allAmiibo.value.length;
    const randomMemory = [];

    for (let i = 0; i < 3; i++) {
        let random = Math.floor(Math.random() * numberAmiibo);
        if(!randomMemory.includes(random)){
            randomMemory.push(random);
            randomAmiiboList.value.push(allAmiibo.value[random]);
        }
        else{
            i--;
        }
    }
}

onBeforeMount(async ()=>{
    await fetchAllAmiibo();
    await getRandomAmiibo();
})



</script>

<template>

    <!-- Banner -->
    <section id="banner">
        <header>
            <h2>Hey.Bienvenue sur ma collection</h2>
        </header>
    </section>

    <!-- Intro -->
    <!-- ici vous pouvez choisir 3 amiibos au hasard ou juste vos trois préférés -->
    <section id="intro" class="container">
        <div class="row">
            <div v-for="amiibo in randomAmiiboList" :key="amiibo.tail" class="col-4 col-12-medium">
                <section @click="pageDetail(amiibo.tail)" class="middle">
                    <img :src="`${amiibo.image}`" />
                    <header>
                        <h2>{{amiibo.character}}</h2>
                    </header>
                    <p>{{amiibo.gameSeries}}</p>
                </section>
            </div>
        </div>
        <footer>
            <ul class="actions">
                <li><a @click="pageList" class="button large">Liste complète</a></li>
            </ul>
        </footer>
    </section>
</template>

<style scoped>
img{
    max-width: fit-content;
}
</style>