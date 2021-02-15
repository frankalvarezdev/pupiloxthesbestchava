<template>
    <div class='error'>
        <div>
            <h1 v-if='error.statusCode === 404'>Pagina no encontrada</h1>
            <!-- <h1 v-else>An error occurred</h1> -->
            <NuxtLink to='/' style='text-align: center; color: #fff'>Regresar al Inicio</NuxtLink>
        </div>
    </div>
</template>

<script>
export default {
    props: ["error"],
    layout: "error", // you can set a custom layout for the error page
};
</script>

<style scoped>
.error {
    display: flex;
    justify-content: center;
}
</style>