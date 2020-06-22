<template>
    <div>
        <div v-if="stage === 'start'">
            <test-main></test-main>
        </div>
        <div v-else-if="stage === 'testing'">
            <test-content></test-content>
        </div>
        <div v-else-if="stage === 'finish'">
            <test-finish></test-finish>
        </div>
    </div>
</template>


<script>
import testMain from "@/components/testMain";
import testContent from "@/components/testContent";
import testFinish from "@/components/testFinish";
export default {
    computed: {
        stage() {
            return this.$store.getters.stage;
        }
    },
    components: {
        testMain,
        testContent,
        testFinish
    }
};
</script>


<style lang="scss">
/*Шрифты*/
@font-face {
    font-family: "Roboto";
    src: url("~@/assets/fonts/Roboto/Roboto-Thin.ttf");
    font-weight: 100;
    font-size: normal;
}
@font-face {
    font-family: "Roboto";
    src: url("~@/assets/fonts/Roboto/Roboto-Light.ttf");
    font-weight: 300;
    font-size: normal;
}
@font-face {
    font-family: "Roboto";
    src: url("~@/assets/fonts/Roboto/Roboto-Regular.ttf");
    font-weight: 400;
    font-size: normal;
}
@font-face {
    font-family: "Roboto";
    src: url("~@/assets/fonts/Roboto/Roboto-Medium.ttf");
    font-weight: 500;
    font-size: normal;
}
@font-face {
    font-family: "Roboto";
    src: url("~@/assets/fonts/Roboto/Roboto-Bold.ttf");
    font-weight: 700;
    font-size: normal;
}
@font-face {
    font-family: "Roboto";
    src: url("~@/assets/fonts/Roboto/Roboto-Black.ttf");
    font-weight: 900;
    font-size: normal;
}
/*общие стили*/
.container-mid {
    font-family: "Roboto";
    max-width: 1060px;
    min-height: 536px;
    margin: 0 auto;
    position: relative;
    left: 0;
    top: 0;
    box-shadow: 0px 30px 40px rgba(133, 73, 86, 0.210598),
        0px 0px 4px rgba(0, 0, 0, 0.0942595);
}
.btn {
    padding: 15px 30px;
    background-color: #fff;
    border-radius: 2px;
    color: #000;
    border: 1px solid #edcdd3;
    &--wrong {
        font-weight: bold;
        color: #e25a76;
        border: 2px solid #e25a76;
    }
    &--correct {
        font-weight: bold;
        color: #43a457;
        border: 2px solid #43a457;
    }
}
.hidden {
    display: none;
}
</style>