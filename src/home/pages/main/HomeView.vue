<template>
    <main-1-page></main-1-page>
</template>

<script>
import { defineComponent } from "vue";
import Main1Page from "../main1/Main1Page.vue";

export default defineComponent({
    name: "HomeView",

    components: { Main1Page },
});
</script>

<style scoped></style>
