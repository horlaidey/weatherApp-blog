<template>
    <div class="form">
        <form @submit="addComment" action="">
            <div class="input">
                <input type="text" placeholder="Enter Display Name" v-model="display">
            </div>
            <div class="input input-comment">
                <textarea placeholder="What do you think" v-model="comment" id="" cols="30" rows="10"></textarea>
            </div>
            <div class="btn">
                <input type="submit" value="POST">
            </div>
        </form>
    </div>
</template>

<script>
    export default{
        name:"Form",
        data(){
            return{
                display:'',
                comment:''
            }
        },
        methods:{
            addComment(e){
                e.preventDefault()
                if(!this.display || !this.comment){
                    alert("Provide a display name and enter your comment")
                }else{

                    const newComment={
                        id: Math.floor(Math.random()*1000),
                        display: this.display,
                        comment: this.comment,
                        time: new Date().toTimeString().slice(0,5)
                    }
                    this.$emit('NewComment', newComment)
                    this.display='',
                    this.comment=''
                }
            }
        }
    }
</script>

<style scoped>
.form{
    background: rgba(0, 0, 0, 0.4);
    border-radius: 10px 10px 0 0;
    padding: 1.5%;
}
.input{
    border-radius: 5px;
}
.btn{
    background: blue;
    border-radius: 5px;
    padding: 5px;
    width: fit-content;
}

</style>