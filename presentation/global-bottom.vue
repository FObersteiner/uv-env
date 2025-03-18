<template>
    <!-- @vue-ignore -->
    <footer 
     v-if="$nav.currentPage !== 7" 
    class="absolute bottom-0 right-0 p-35px"
    >
    f.obersteiner: uv
    </footer>
</template>

<style>
    footer {
        position: absolute;
        bottom: 35px;
        right: 35px;
        width: calc(100% - 20px);
        text-align: right;
        font-size: 0.8em;
        color: #888;
    }
</style>