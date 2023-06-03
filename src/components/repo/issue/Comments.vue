<template>
    <div>
        <div>
            <h4>Comments</h4>
            <div v-for="c of comments" :key="c.id">
                {{ c.user && c.user.login }} - {{ c.body }}
            </div>
        </div>
    </div>
</template>
<script>
    import { octokitMixin } from '../../../mixins/octokitMixin';

    export default{
        name: "IssueComments",
        props : {
            owner: {
                type: String,
                required: true
            },
            repo: {
                type: String,
                required: true
            },
            issueNumber: {
                type: Number, 
                required: true
            }
        },
        data(){
            return {
                comments: []
            }
        }, 
        mixins: [octokitMixin],
        methods: {
            async getIssueComments(owner, repo, issueNumber){
                if( 
                    typeof owner != "string" ||
                    typeof repo != "string" || 
                    typeof issueNumber != "number"){
                    return;
                }

                const octokit = this.createOctokitClient();
                const {data: comments} = await octokit.issues.listComments({
                    owner, repo, issue_number: issueNumber
                })

                this.comments = comments
            }

        }
    }
</script>