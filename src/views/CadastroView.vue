<template>
    <div>
        <NavBar/>
        <Cadastro/>
    </div>
</template>


<script>
import Cadastro from '../components/Cadastro.vue';
import NavBar from '../components/NavBar.vue';
export default{
components: {
    Cadastro,
    NavBar
}
}

</script>