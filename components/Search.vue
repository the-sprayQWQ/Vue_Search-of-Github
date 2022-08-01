<template>
      <section class="jumbotron">
      <h3 class="jumbotron-heading">Search Github Users</h3>
      <div>
        <input type="text" placeholder="enter the name you search" v-model="keyword"/>&nbsp;
        <button @click="searchUsers">Search</button>
      </div>
    </section>
</template>

<script>
import axios from 'axios'
export default {
    name:'Search',
    data() {
        return {
            keyword:''
        }
    },
    methods: {
        searchUsers(){
            //请求前更新list数据
            this.$bus.$emit('updateListData',{isFirst:false,isLoading:true,errMsg:'',users:[]})
            axios.get(`https://api.github.com/search/users?q=${this.keyword}`).then(
                Response =>{
                    //请求成功后
                    this.$bus.$emit('updateListData',{isLoading:false,errMsg:'',users:Response.data.items})
                },
                error =>{
                    //请求失败后
                    this.$bus.$emit('updateListData',{isLoading:false,errMsg:error.message,users:[]})
                }
            )
        }
    },
}
</script>

<style>

</style>