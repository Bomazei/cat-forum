<template>
<div>
    <div class="post">
        <img src="https://placekitten.com/200/200" alt="post-author">
        <div class="post-content">
            {{users[post.userId-1].name}}
            <p class="post-title">{{post.title}}</p>
            <p class="post-body">{{post.body}}</p>
        </div>
        
        <button @click="showComments(post.id), close = true" v-if="!close" class="comment-open">Открыть комментарии</button>
    </div>
    <ul v-if="close" class="comments">
        <li v-for="comment in comments" :key="comment.id" class="comment">
            <img src="https://placekitten.com/50/100" alt="comment-author" class="comment-image">
            <div class="comment-content">
                <p class="comment-name">{{comment.name}}</p>
                <p class="comment-body">{{comment.body}}</p>
            </div>
            <span v-if="comment.name == ''">NO</span>
        </li>  
    <button @click="close = false" v-if="close" class="comment-close">Закрыть комментарии</button>
    </ul>
</div>
  
</template>

<script>
export default {
    props: ["post", "users"],
    data(){
        return{
            comments: null,
            close: false,
        }
    },
    methods:{
        showComments: function(id){
        fetch('https://jsonplaceholder.typicode.com/comments?postId='+id)
        .then(response => (response.json()))
        .then(json => this.comments = json)
        }
    }
}
</script>

<style>

</style>