<script setup>

import { onBeforeMount,ref } from 'vue';
import axios from 'axios';
import {useRouter} from 'vue-router';

const allAmiibo = ref()
const numberAmiibo = ref(0)
const router = useRouter()

const pageDetail = (id) =>{
    router.push({name:'detail',params:{id}})
}

const fetchAllAmiibo = async()=>{
    const amiibos = await axios.get('https://www.amiiboapi.com/api/amiibo/')
    const {data,status} = amiibos
    // console.log(amiibos)
    if(status == 200){
        allAmiibo.value = data.amiibo;
    }
    else{
        console.warn(status)
    }

}

const countAmiibo = async() =>{
    // console.log(allAmiibo.value.length);
    numberAmiibo.value = allAmiibo.value.length;
}

onBeforeMount(async ()=>{
    await fetchAllAmiibo();
    await countAmiibo();
})

</script>

<template>
    <!-- Main -->
    <section id="main">
        <div class="container">

            <!-- Content -->
                <article class="box post">
                    
                    <header>
                        <h2>Ma Collection</h2>
                        <p>{{numberAmiibo}} amiibos</p>
                    </header>
                    <p>
                        <table>
                            <tr>
                                <th>Character</th>
                                <th>game Series</th>
                                <th>Action</th>
                            </tr>
                            <tr v-for="amiibo in allAmiibo" :key="amiibo.tail">
                                <td>{{ amiibo.character }}</td>
                                <td>{{ amiibo.amiiboSeries }}</td>
                                <td><button @click="pageDetail(amiibo.tail)">voir</button></td>
                            </tr>
                        </table>
                    </p>
                    
                </article>

        </div>
    </section>
</template>
