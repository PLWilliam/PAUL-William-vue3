<script setup>
import {ref,computed,reactive} from 'vue';
import {useRouter} from 'vue-router'

const props = defineProps({
        status:Boolean
    }
)

const emit = defineEmits(['homeClick','listClick'])

const router = useRouter();

const name = ref('');
const current = ref(props.status);

const pageHome = () =>{
    // current.value=true;
    emit('homeClick',true)
    // props.status=true;
    router.push({name:'home'});
}

const pageList = () =>{
    // current.value=false;
    emit('homeClick',false)
    // props.status=false;
    router.push({name:'list'});
}

const statusState = computed(()=>{
    // current.value = props.status
    return props.status
})

</script>

<template>
    <!-- Header -->
    <section id="header">
        <!-- {{ statusState }} -->
        {{ name }}
        <!-- Logo -->
        <h1><a @click="pageHome">AmiiVue</a></h1>

        <!-- Nav -->
        <nav id="nav">
            <ul>
                <li class="btn" :class="status?'current':''"><a @click="pageHome">Home</a></li>
                <li class="btn" :class="!status?'current':''"><a @click="pageList">Liste Amiibo</a></li>
            </ul>
        </nav>
            <!-- Banner -->
        <section id="banner" v-if="status">
            <header>
                <h2>Hey.Bienvenue sur ma collection</h2>
            </header>
        </section>
        
    </section>
</template>

<style scoped>
.btn:hover{
    cursor: pointer;
}
</style>