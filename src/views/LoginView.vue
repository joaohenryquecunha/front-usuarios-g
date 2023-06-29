<template>
<div>
    <NavBar/>
    <Login/>
</div>
</template>

<script>
import Login from '../components/Login.vue'
import NavBar from '../components/NavBar.vue'
export default {
    components: {
        Login,
        NavBar
    }
}
</script>