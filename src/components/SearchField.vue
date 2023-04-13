<template>
    <div class="inputWrapper">
        <div class="icon">
            <img  class="searchIcon" src="../assets/search-normal.svg" />
        </div>
        <input class="searchInput d-none d-md-block" type="text" placeholder="Search" />
    </div>
</template>

<script>
import SearchIconVue from './icons/SearchIcon.vue'

export default {
    name: 'SearchField',
    components: { SearchIconVue }
}
</script>

<style scoped>
.searchInput {
    background: #1B1F32;
    border: 1px solid #494D61;
    border-radius: 6px;
    height: 40px;
    width: 331px;
    color: #fff;
    padding-left: 28px;
}

.inputWrapper {
    position: relative;
}

.icon {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 8.73px;
    z-index: 2;
    display: flex;
    align-items: center;
    justify-content: center;
}

@media (max-width: 766px) {
    .icon {
        position: relative;
    }
    .searchIcon {
        width: 24px;
    }
}
</style>