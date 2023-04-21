<script setup>
import {ref} from 'vue';
import {useRouter} from 'vue-router'

const router = useRouter();

const name = ref('');
const current = ref(true);

const pageHome = () =>{
    router.push({name:'home'});
    current.value=true;
}

const pageList = () =>{
    router.push({name:'list'});
    current.value=false;
}


</script>

<template>
    <!-- Header -->
    <section id="header">
        {{ name }}
        <!-- Logo -->
        <h1><a @click="pageHome">AmiiVue</a></h1>

        <!-- Nav -->
        <nav id="nav">
            <ul>
                <li class="btn" :class="current?'current':''"><a @click="pageHome">Home</a></li>
                <li class="btn" :class="!current?'current':''"><a @click="pageList">Liste Amiibo</a></li>
            </ul>
        </nav>
        
    </section>
</template>

<style scoped>
.btn:hover{
    cursor: pointer;
}
</style>