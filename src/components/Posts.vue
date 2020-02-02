<template>
    <div>
        <ul class="container">
            
            <li v-for="post in postsFiltered" :key="post.id">
                
                
                <Post :post="post" :users="users">
                    
                </Post>
                
            </li>
        </ul>
        <div class="filters">
            <p class="filters-title">Фильтры:</p>
            <p class="filter-name">Имя/название</p>
            <input type="text" class="filter-input" v-model="searchName">
            <p class="filter-name">Контент</p>
            <input type="text" class="filter-input" v-model="searchContent">
        </div>
    </div>
  
</template>

<script>
import Post from './Post'
export default {
    data(){
        return{
            posts: [],
            users: [],
            searchName: '',
            searchContent: '',
        }
    },
    beforeMount(){
        fetch('https://jsonplaceholder.typicode.com/posts')
            .then(response => (response.json()))
            .then(json => {
                this.posts = json
            })
        fetch('https://jsonplaceholder.typicode.com/users')
            .then(response => (response.json()))
            .then(json => {
                this.users = json
            })   
           
    },
    computed: {
        postsFiltered() { 
            return this.posts.filter(post => post.body.indexOf(this.searchContent) !== -1)  
        },
        usersFiltered() {
            return this.users.filter(user => user.name.indexOf(this.searchName) !== -1)
        }
    },
    components:{
        Post
    } 
}
</script>

<style>

</style>