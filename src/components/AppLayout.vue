<script>
import Header from './Header.vue'
export default {
    name: 'AppLayout',
    components: { Header }
}
</script>

<template>
    <Header/>
    <slot></slot>
</template>
