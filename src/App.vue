<template>
    <div id="app">
        <app-test></app-test>
    </div>
</template>

<script>
import appTest from "@/components/appTest";
// import { mapActions } from "vuex";
export default {
    // methods: {
    //     ...mapActions(["get_questionsLists_from_api"])
    // },
    // mounted() {
    //     this.get_questionsLists_from_api();
    // },
    components: {
        appTest
    }
};
</script>
<style lang="scss">
/*сброс стилей*/
html,
body {
    height: 100%;
    width: 100%;
    font-size: 16px;
    line-height: 1;
}
*,
*::before,
*::after {
    margin: 0;
    padding: 0;
    border: 0;
    box-sizing: border-box;
}
button {
    cursor: pointer;
}
a,
a:visited,
a:hover,
a:active {
    text-decoration: none;
}
</style>
