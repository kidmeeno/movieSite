<script>
import HeaderVue from './Header.vue'

export default {
    name: "Layout",
    components: { HeaderVue }
}
</script>

<template>
    <HeaderVue/>
    <slot></slot>
</template>

<style>

</style>