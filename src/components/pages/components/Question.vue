<template>
    <div class="bg-white p-12 rounded-lg shadow-lg w-full mt-8">
        <div>
            <p class="text-2xl font-bold">{{ question }}</p>
            <label
                v-for="(text, key) in answers"
                :key="key"
                :for="'answer-' + key"
                class="block mt-4 border border-gray-300 rounded-lg py-2 px-6 text-lg hover:bg-gray-100 cursor-pointer"
                :class="{'bg-green-200': answer == key}"
            >
                <input
                    :id="'answer-' + key"
                    v-model="answer"
                    type="radio"
                    class="hidden"
                    :value="key"
                /> {{ text }}
            </label>
            <div class="mt-6 flow-root">
                <button
                    v-if="answer && !isLastQuestion"
                    v-on:click="emitAnswer"
                    class="float-right bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full px-5 py-2"> Next &gt;
                </button>
                <button
                    v-on:click="emitAnswer"
                    v-if="answer && isLastQuestion"
                    class="float-right bg-indigo-600 text-white text-sm font-bold tracking-wide rounded-full px-5 py-2"> Finish
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            question: {
                type: String,
                required: true
            },
            isLastQuestion: {
                type: Boolean,
                default: false
            }
        },
        data() {
            return {
                answer: null,
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
            emitAnswer() {
                const data = {
                    question: this.question,
                    answer: this.answer
                }

                this.answer = null

                this.$emit('answer', data)
            }
        },
        computed: {

        },
        mounted() {
        }
    };
</script>
<style lang="scss" scoped>
</style>