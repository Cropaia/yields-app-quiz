<template>
<div>
    <navbar>
        <div class="columns">
            <div class="column">
                <div class="btn-group btn-group-block">
                    <button  v-for="(question, index) in questions" :key="index"
                        class="btn" @click="scrollTo(index)">{{ index + 1 }}</button>
                </div>
            </div>
            <div class="column" style="flex-grow: 0;">
                <button class="btn" @click="close">{{ $t("close") }}</button>
            </div>
        </div>
    </navbar>
    <div class="big-number">{{ correctPercent }}</div>
    <form @submit.prevent>
        <template v-for="(question, index) in questions">
            <h3 ref="header" v-if="!question.results">{{ $t("question_x_result", {num: index + 1, correct: question.correct_tasks, total: question.total_tasks }) }}</h3>        
            <snippet v-for="snippet in question.content" :key="index" :snippet="snippet" />
        </template>
    </form>
</div>
</template>

<script>
declare var require: any;

const ResultSnippet = require('./ResultSnippet.vue').default;
const Navbar = require("./Navbar.vue").default;

export default {
    props: ["questions"],
    data() {
        return {};
    },
    methods: {
        close() {
            this.$emit("close");
        },
        scrollTo(index) {
            const questionHeader = this.$refs.header[index];
            const NAVBAR_HEIGHT = 60;

            // document.body.scrollTop is deprecated.
            // Instead, document.scrollingElement should be used for Chrome,
            // Firefox and Edge.
            // MSIE only supports document.documentElement.
            // https://miketaylr.com/posts/2014/11/document-body-scrolltop.html
            // https://developer.mozilla.org/en-US/docs/Web/API/document/scrollingElement
            (document.scrollingElement || document.documentElement).scrollTop +=
                questionHeader.getBoundingClientRect().top - NAVBAR_HEIGHT;
        }
    },
    computed: {
        correctPercent() {
            let firstResult =this.questions.find(q=>q.results!=null);
            const total = this.questions
            .map((q) => q.total_tasks)
            .reduce((a, b) => a + b, 0);

            const correct = this.questions
            .map((q) => q.correct_tasks)
            .reduce((a, b) => a + b, 0);

             if(firstResult){
               firstResult= firstResult.results;
               for(var result in firstResult){
                   var resultValues=firstResult[result];
                   if(resultValues.includes(correct))
                        return result;
               }
               return "Not Found, Please try again";
            }

            return Math.round(correct / total * 100).toString() + " %";
        }
    },
    components: {
        "snippet": ResultSnippet,
        "navbar": Navbar
    }
}
</script>

<style>
.big-number {
    margin: auto;
    text-align: center;
    vertical-align: middle;
    font-size: 6rem;
    display: block;
    border-radius: 1rem;
    background-color: #fcac14;
}
</style>
