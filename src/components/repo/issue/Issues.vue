<template>

</template>
<script>
    import { octokitMixin } from '../../../mixins/octokitMixin';
    import IssueComments from "./../issue/Comments.vue"

    export default{
        name: "RepoIssues",
        components: {
            IssueComments,
        },
        props: {
            owner: {
                type: String,
                required: true
            },
            repo: {
                type: String,
                required: true
            },
        },
        mixins: [octokitMixin],
        data(){
            return{
                issues: [],
                showIssues: false
            }
        },
        methods: {
            async getRepoIssues(owner, repo){
                const octokit = this.createOctokitClient();
            }
        }
    }
</script>