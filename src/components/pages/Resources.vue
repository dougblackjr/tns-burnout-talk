<template>
    <section class="w-full max-w-5xl m-auto mt-16">
        <h2 class="text-2xl font-bold">Resources For Help</h2>
        <p class="text-sm mt-4">A list of lists of resources to help you, from experts around the world.</p>
        <div class="my-8 flex flex-col">
            <a 
                v-for="(resource, idx) in resources"
                :key="idx"
                :href="resource.url"
                :title="resource.title"
                target="_blank"
                class="mb-8"
            >
                {{ resource.title }}
            </a>
        </div>
    </section>
</template>

<script>
    export default {
        components: {},
        props: {},
        data() {
            return {
                resources: [
                    {
                        title: 'Mental Health Resources to Help Prevent Creative and Professional Burnout',
                        url: 'https://bootcamp.berkeley.edu/blog/mental-health-resources-to-help-prevent-creative-and-professional-burnout/'
                    },
                    {
                        title: 'Well Being Resources',
                        url: 'https://www.psychiatry.org/psychiatrists/practice/well-being-and-burnout/well-being-resources'
                    },
                    {
                        title: 'NAMI Mental Health Workplace Kit',
                        url: 'https://static1.squarespace.com/static/5e1c87de79b1df2af20bc895/t/5ec6c478a211ce4796ab15cc/1590084733899/NAMI_Mental+Health+Workpl%20ace+Toolkit_v3+%281%29.pdf'
                    },
                ]
            }
        },
        methods: {

        },
        computed: {

        },
        mounted() {
        }
    };
</script>
<style lang="scss" scoped>
</style>