<template>
    <RecipePreviewList class="RecipePreviewList" title="Your last viewed recipes"  :recipes="this.recipes"/>
</template>

<script>
    import RecipePreviewList from "./RecipePreviewList";

    export default {
        name: "LastViewedRecipePreviewList",
        components: {
            RecipePreviewList
        },
        data() {
            return {
                recipes: []
            };
        },
        async created() {
            try {
                const response = await this.axios.get(
                    this.$root.store.prefixURL + "/user/getLastViewed",
                    {withCredentials: true}
                );
                const recipes = response.data;
                this.recipes = [];
                this.recipes.push(...recipes);
                for (let i = 0; i < this.recipes.length; i++) {
                    this.recipes[i].watched = "";
                    this.recipes[i].saved = "";
                }
            } catch (error) {
                console.log(error);
            }
        }
    }


</script>

<style scoped>
    .RecipePreviewList.title{
        font-family: Calibri;
        font-weight: bold;
        size: 22px;
    }

</style>