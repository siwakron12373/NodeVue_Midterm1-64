<template>
<div>
    <h1>Edit Song</h1>
    <form v-on:submit.prevent = "editUser">
        <p>ชื่อเพลง: <input type="text" v-model="user.name"></p>
        <p>ลิงค์เพลง: <input type="text" v-model="user.lastname"></p>
        <p>email: <input type="text" v-model="user.email"></p>
        <p>ชื่อนักร้อง: <input type="text" v-model="user.password"></p>
        <p><button type="submit">edit Song</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อเพลง: {{user.name}}</p>
        <p>ลิงค์เพลง: {{user.lastname}}</p>
        <p>email: {{user.email}}</p>
        <p>ชื่อนักร้อง: {{user.password}}</p>
    </div>
</div>
</template>
<script>import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async editUser(){
            try{
                await UsersService.put(this.user)
                this.$router.push({
                    name: 'users'
                })

            }catch(error){
                console.log(error)
            }
        }
    }, 
    async created(){
        try{
            let userId = this.$route.params.userId
            this.user = (await UsersService.show(userId)).data
        }catch(error){
            console.log(error)
        }
    }
}
</script>
<style scoped>


</style>