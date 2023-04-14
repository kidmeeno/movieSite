<script>
import SearchField from '../components/SearchField.vue';
export default {
    name: "Header",
    components:{SearchField}
}
</script>

<template>
    <header class="header">
        <nav>
            <router-link to="/"> <img class="logo" src="../assets/Logo.svg" /></router-link>
            <SearchField/>
        </nav>
    </header>
</template>

<style scoped>
.header {
    height: 80px;
    position: fixed;
    top: 0;
    right: 0;
    left: 0;
    background: #1D283C;
    z-index: 3;
}

nav {
    max-width: 1280px;
    margin: 20.5px auto;
    display: flex;
    padding: 0 2rem;
    justify-content: space-between;
}

@media (max-width: 766px) {
    .logo {
        width: 94px;
        height: 32px;
    }
}
</style>