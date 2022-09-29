<template>
    <section class="w-full max-w-5xl m-auto mt-4">
        <div v-if="shouldShowQuestions">
            <question 
                :question="currentQuestion"
                :is-last-question="isLastQuestion"
                v-on:answer="answerQuestion"
            />
        </div>
        <div v-if="!shouldShowQuestions">
            <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-8">
                <div>
                    <h2 class="text-bold text-3xl">Results</h2>
                    <div class="flex flex-col justify-start space-x-4 mt-6">
                        <p>Your Score: <span class="text-2xl text-green-700 font-bold">{{ cumulativeScore }}</span></p>
                        <p>Result: <span class="text-2xl text-red-700 font-bold">{{ scoreResult }}</span></p>
                        <div class="my-4">
                            <a v-on:click="$emit('change-page', 'resources')" href="#" >View Resources</a>
                        </div>
                        <div class="my-4">
                            <p>Scores:</p>
                            <p
                                v-for="(s, idx) in scores"
                                :key="idx"
                                class="text-gray-800"
                            >
                                <span class="font-bold">{{ s.question }}</span><br />
                                {{ this.answers[parseInt(s.answer)]}}
                            </p>
                        </div>
                    </div>
                    <div class="mt-6 flow-root">
                        <button v-on:click="resetAssessment" class="float-right bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full px-5 py-2"> Reset </button>
                    </div>
                </div>
            </div>
        </div>
        <p class="text-xs mt-4">More information on this assessment can be found at <a href="https://www.astrazeneca.com/content/dam/az/PDF/2020/covid-19-toolkit/Burnout_Self-Test.pdf" target="_blank">https://www.astrazeneca.com/content/dam/az/PDF/2020/covid-19-toolkit/Burnout_Self-Test.pdf</a>. This does not constitute medical advice, and is not sponsored by any medical organization.</p>
    </section>
</template>

<script>
    import Question from './components/Question.vue'
    export default {
        components: {
            Question
        },
        props: {},
        data() {
            return {
                scores: [],
                shouldShowQuestions: true,
                cumulativeScore: 0,
                currentQuestionIndex: 0,
                questions: [
                    'I feel run down and drained of physical or emotional energy.',
                    'I have negative thoughts about my job.',
                    'I am harder and less sympathetic with people than perhaps they deserve.',
                    'I am easily irritated by small problems, or by my co-workers and team.',
                    'I feel misunderstood or unappreciated by my co-workers.',
                    'I feel that I have no one to talk to.',
                    'I feel that I am achieving less than I should.',
                    'I feel under an unpleasant level of pressure to succeed.',
                    'I feel I am not getting what I want out of my job.',
                    'I feel that I am in the wrong organization or the wrong profession.',
                    'I am frustrated with parts of my job.',
                    'I feel that organizational politics or bureaucracy frustrate my ability to do a good job.',
                    'I feel that there is more work to do than I practically have the ability to do.',
                    'I feel that I do not have time to do many of the things that are important to doing a good quality job.',
                    'I find that I do not have time to plan as much as I would like to.',
                ],
                scoringThreshholds: [
                    {
                        'min': 0,
                        'max': 18,
                        'message': 'No sign of burnout here'
                    },
                    {
                        'min': 19,
                        'max': 32,
                        'message': 'Little sign of burnout here, unless some factors are particularly severe.'
                    },
                    {
                        'min': 33,
                        'max': 49,
                        'message': 'Be careful – you may be at risk of burnout, particularly if several scores are high.'
                    },
                    {
                        'min': 50,
                        'max': 59,
                        'message': 'You are at severe risk of burnout – do something about this urgently.'
                    },
                    {
                        'min': 60,
                        'max': 9999,
                        'message': 'You are at very severe risk of burnout – do something about this urgently.'
                    }
                ],
                answers: {
                    1: 'Not at All',
                    2: 'Rarely',
                    3: 'Sometimes',
                    4: 'Often',
                    5: 'Very Often'
                }
            }
        },
        methods: {
            resetAssessment() {
                this.scores = []
                this.cumulativeScore = 0
                this.currentQuestionIndex = 0
            },
            answerQuestion(data) {
                console.log('data', data)
                this.scores.push(data)
                this.cumulativeScore += parseInt(data.answer)
                this.currentQuestionIndex++

                if (this.currentQuestionIndex === this.questions.length) {
                    this.shouldShowQuestions = false
                }
            }
        },
        computed: {
            currentQuestion() {
                return this.questions[this.currentQuestionIndex]
            },
            scoreResult() {
                const threshold = this.scoringThreshholds.find(s => {
                    return s.min <= this.cumulativeScore && s.max >= this.cumulativeScore
                })
                console.log('threshold', threshold, this.cumulativeScore)
                if (threshold) {
                    return threshold.message
                }

                return ''
            },
            isLastQuestion() {
                return this.currentQuestion === this.questions[this.questions.length - 1]
            }
        }
    };
</script>
