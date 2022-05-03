<template>
    <div class="my-10 pb-12 mx-96 bg-white-200 shadow-lg">
        <h2 class="text-4xl text-red-900 font-bold font-serif py-10">Sign Up</h2>
        <div class="register text-red-900 font-bold border-2">
            <table align="center">
                <tr>
                    <td>Name : </td>
                    <td><input type="text" class="w-72 p-2 rounded-xl" v-model="name" placeholder=" Enter Name" /></td>
                </tr><br>
                <tr>
                    <td>Email ID : </td>
                    <td><input type="email" class="w-72 p-2 rounded-xl" v-model="email" placeholder=" Enter Email" /></td>
                </tr><br>
                <tr>
                    <td>Password : </td>
                    <td><input type="password" class="w-72 p-2 rounded-xl" v-model="password" placeholder=" Enter Password" /></td>
                </tr><br>
            </table>
            <button v-on:click="signUp" class="bg-red-900 text-white px-4 py-2 rounded-3xl">Sign Up</button>
            
            <div class="mt-10 text-blue-700">
                <p class="text-xs">Already have an account? </p>
                <router-link to="/login" class="text-red-700">LOGIN</router-link>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
    name :'SignUp',
    data()
    {
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        async signUp()
        {
            let result = await axios.post("http://localhost:3000/users", {
                email:this.email,
                password:this.password,
                name:this.name
            });

            console.warn(result);
            if(result.status==201)
            {
                // alert("sign up succesfull");
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted()  
    {
        let user=localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name:'Home'})
        }
    }
}
</script>
