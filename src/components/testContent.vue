<template>
    <div class="testContent">
        <div class="container-mid">
            <div class="testContent__wrapper">
                <div class="testContent__content">
                    <span class="testContent__pagination">{{currentPage}}/{{questionsListsLength}}</span>
                    <h3 class="testContent__title">{{questionsLists[currentPage - 1].question}}</h3>
                    <div class="testContent__option">
                        <button
                            class="testContent__option-item btn"
                            v-for="(item, idx) in questionsLists[currentPage - 1].content"
                            :key="idx"
                            @click="toChoice($event)"
                            :disabled="btnDisabled"
                            ref="testContentBtn"
                        >{{item.answer}}</button>
                    </div>

                    <template v-if="showDescrip">
                        <div class="testContent__description">{{getAnswerText}}</div>

                        <button class="testContent__continue" @click="nextPage">{{textContinue}}</button>
                    </template>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import { mapGetters } from "vuex";
export default {
    data() {
        return {
            showDescrip: false,
            btnDisabled: false,
            textContinue: "Продолжить"
        };
    },
    computed: {
        ...mapGetters([
            "currentPage",
            "questionsLists",
            "getAnswerText",
            "questionsListsLength"
        ])
    },
    methods: {
        nextPage() {
            if (this.textContinue == "Завершить") {
                this.$store.dispatch("toTesting", "finish");
            } else {
                this.$store.dispatch("nextPage");
            }
            this.$refs.testContentBtn.forEach(element => {
                element.classList.remove(
                    "hidden",
                    "btn--correct",
                    "btn--wrong"
                );
            });
            this.btnDisabled = false;
            this.showDescrip = false;
            if (this.currentPage === this.questionsListsLength) {
                this.textContinue = "Завершить";
            }
        },
        toChoice(e) {
            let answers = this.questionsLists.map(item => {
                return item.content;
            });
            let currentAnswer = answers[this.currentPage - 1];
            let rightAnswers = []; //answer true

            for (let i = 0; i < currentAnswer.length; i++) {
                if (currentAnswer[i].correct === true) {
                    rightAnswers.push(currentAnswer[i].answer);
                }
            }
            for (let i = 0; i < rightAnswers.length; i++) {
                if (rightAnswers[i] === e.target.innerHTML) {
                    e.target.classList.add("btn--correct");
                    this.$refs.testContentBtn.forEach(element => {
                        element.classList.add("hidden");
                    });
                    e.target.classList.remove("hidden");
                    this.btnDisabled = true;
                    this.showDescrip = true;
                    this.$store.dispatch("addRightAnswers");
                } else {
                    e.target.classList.add("btn--wrong");
                    this.$refs.testContentBtn.forEach(element => {
                        element.classList.add("hidden");
                    });
                    e.target.classList.remove("hidden");
                    this.btnDisabled = true;
                    this.showDescrip = true;
                }
            }

            for (let i = 0; i < currentAnswer.length; i++) {
                if (e.target.innerHTML === currentAnswer[i].answer) {
                    this.$store.dispatch(
                        "getAnswerText",
                        currentAnswer[i].description
                    );
                }
            }
        }
    }
};
</script>


<style lang="scss">
.testContent {
    &__wrapper {
        background: url("~@/assets/images/start-bg-pink.jpg") no-repeat;
        background-size: cover;
    }
    &__content {
        min-height: 536px;
        max-width: 500px;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        padding: 30px 20px 45px 20px;
    }
    &__pagination {
        margin: 0 0 15px 0;
        line-height: 19px;
    }
    &__title {
        margin: 0 0 30px 0;
        font-weight: 500;
        font-size: 26px;
        line-height: 36px;
    }
    &__option {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        &-item {
            display: inline-block;
            margin: 0 0 10px 0;
            line-height: 19px;
            &:last-child {
                margin: 0;
            }
        }
    }

    &__description {
        margin: 30px 0 20px 0;
        line-height: 23px;
        span {
            font-weight: bold;
        }
        a {
            text-decoration: underline;
        }
    }

    &__continue {
        margin-top: auto;
        font-weight: bold;
        font-size: 20px;
        line-height: 23px;
        background: transparent;
        position: relative;
        outline: none;
        &::after {
            content: "";
            margin: 0 0 0 15px;
            position: relative;
            right: 0;
            top: 3px;
            display: inline-block;
            width: 25px;
            height: 20px;
            background-image: url("~@/assets/images/Group 12.svg");
        }
    }
}
</style>