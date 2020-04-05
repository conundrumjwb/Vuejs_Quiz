<template>
    <div class="quiz-results-container">
        <b-jumbotron>
            <template v-slot:lead>End of Quiz Results</template>
            <hr class="my-4">
            <p>
                Number of answered questions: {{ numTotal }}
            </p>
            <p>
                Number of corretly answered questions: {{ numCorrect }}
            </p>
            <p>
                Success percentage: {{ resultPercentage }}%
            </p>

            <b-button variant="primary" @click="reloadPage">New Quiz</b-button>
        </b-jumbotron>
    </div>
</template>

<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ],
    data() {
        return {
            resultPercentage: this.numCorrect / this.numTotal * 100
        }
    },
    methods: {
        reloadPage() {
            window.location.reload()
        }
    }
}
</script>