<template>
    <div class="testMain">
        <div class="container-mid">
            <div class="testMain__wrapper">
                <div class="testMain__content">
                    <span class="testMain__flag">Текст</span>
                    <h2 class="testMain__title">Как хорошо вы разбираетесь в новостях бизнеса</h2>
                    <p class="testMain__text">По следам публикаций на vc.ru.</p>
                    <button class="testMain__btn btn" @click="toTesting">Начать</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    methods: {
        toTesting() {
            this.$store.commit("toTesting", "testing");
        }
    }
};
</script>

<style lang="scss">
.testMain {
    &__wrapper {
        background: url("~@/assets/images/startWin-bg.png") no-repeat;
        background-size: cover;
    }
    &__content {
        max-width: 560px;
        min-height: 536px;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding: 70px 50px 40px 50px;
    }
    &__title {
        font-weight: 900;
        font-size: 34px;
        line-height: 40px;
        margin: 0 0 20px 0;
    }
    &__text {
        font-size: 18px;
        line-height: 27px;
    }
    &__flag {
        display: inline-block;
        align-self: flex-end;
        padding: 7px 13px;
        color: #fff;
        background-color: #e25a76;
        position: relative;
        margin: 0 0 15px 0;
        &::after {
            content: "";
            position: absolute;
            bottom: -15px;
            right: 0;
            width: 0;
            height: 0;
            border-top: 15px solid #ba4961;
            border-right: 15px solid transparent;
        }
    }
    &__btn {
        margin-top: auto;
        font-weight: bold;
        font-size: 20px;
        line-height: 23px;
        outline: none;
        &.btn {
            border: none;
        }
    }
}
</style>