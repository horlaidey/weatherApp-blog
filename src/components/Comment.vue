<template>
    <div class="comment">
        <div :key="comment.name" class="interaction" v-for="comment in comments">
            <div class="header">
                {{comment.display}} <span>{{comment.time}}</span>
            </div>
            <div class="content">
                {{comment.comment}}
            </div>
        </div>
        <div v-if="showForm">
            <Form @NewComment="addComment" />
            <button @click="toggleForm" class="red">&#10006;</button>
        </div>
        <div v-else @click="toggleForm" class="addComment">
            Post Comment
        </div>
    </div>
</template>

<script>
import {getDatabase, ref, set, get, child, onValue, remove, update} from "firebase/database"
import {db} from '../db'
import Form from './Form.vue'

const datbas = getDatabase(db);
const dbRef = ref(getDatabase(db));

    export default{
        name:'Comment',
        components:{
            Form
        },
        data(){
           return{
            comments:[],
            showForm: false,
            userName:"",
            message:"",
            time:""
           }
        },
        methods:{
           
            addComment(inputs){
                set(ref(datbas,`post/${inputs.id}`), inputs)
                this.toggleForm()
            },
            toggleForm(){
                this.showForm = !this.showForm
            },
             
                appendComment(comment){
                    this.comments = comment
                }
                
                
            },
         created(){
             onValue(dbRef, (snapshot) => {
                get(child(dbRef, 'post')).then((snapshot)=>{
                   var post = [];
                    snapshot.forEach(childSnapshot => {
                        post.push(childSnapshot.val());
                      this.appendComment(post)
                    })
                })
             });
        }
    }
</script>

<style scoped>
    .addComment{
        width: fit-content;
        display: inline-block;
        cursor: pointer;
        background: rgb(141, 169, 221);
        color: #fff;
        border-radius: 20px;
        padding: 10px;
    }
    .comment{
        background: #fff;
        border-radius: 10px;
        padding: 2.5%;
        margin: auto;
        width: 60%;
        margin-bottom: 0;
    }
   
    .interaction{
        position: relative;
        padding: 2.5%;
        border-radius: 10px 10px 0 0;
        display: flex;
        flex-direction: column;
        border-bottom: rgba(158, 158, 231, 0.178) 2px solid;
    }
    .header{
        font-weight: bolder;
        color: #874601;
        width: fit-content;
        padding: 5px;
        border-bottom-style:groove;
        margin-left: 0;
        margin-bottom: 2.5%;
    }
    .header span{
        padding: 5px;
        width: fit-content;
        font-weight: lighter;
        font-style: italic;
        text-align: end;
        color: rgb(127, 194, 194);
        border-style: inset;
        border: 0;
        background: rgba(217, 215, 215, 0.795);
        border-radius: 10px;
    }
    .content{
        padding: 2%;
        max-width: auto;
        border-radius: 5px;
        background: rgba(141, 169, 211, 0.2);
        margin-left: 5%;
    }
    .icons{
        position: absolute;
        right: 5%;
        color: #874601;
        cursor: pointer;
        font-size: medium;
        font-weight: bolder;
    }
    .red{
        color: red;
        font-style: italic;
    }

    @media only screen and (max-width:480px){
        .comment{
            width: 100%;
            padding: 5%;
            border-radius: 20px 20px 0 0;
        }
        .interaction{
            padding: 5%;
        }
    }
    
</style>