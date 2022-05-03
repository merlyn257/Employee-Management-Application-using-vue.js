<template>
    <div class="bg-white shadow-xl ring-1">
        <h2 class="text-4xl text-red-900 font-bold py-10">Log In</h2>
        <div class="text-red-900 font-bold border-2">
            <table align="center">
                <tr>
                    <td>Email ID : </td>
                    <td><input type="email" class="w-72 p-2 rounded-xl" v-model="email" placeholder=" Enter Email" /></td>
                </tr><br>
                <tr>
                    <td>Password : </td>
                    <td><input type="password" class="w-72 p-2 rounded-xl" v-model="password" placeholder=" Enter Password" /></td>
                </tr><br>
            </table>
        </div>

        <button v-on:click="login" class="bg-red-900 text-white px-4 py-2 rounded-3xl">Log In</button>
        
        <div class="mt-10 text-blue-700">
            <p class="text-xs">Don't have an account? </p>
            <router-link to="/sign-up" class="text-red-700">SIGN UP</router-link>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
export default{
    name:'Login',
    data()
    {
        return{
            email:'',
            password:''
        }
    },
    methods:{
        async login()
        {
            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`
            )
            if(result.status==200 && result.data.length)
            {
			localStorage.setItem("user-info",JSON.stringify(result.data[0]))
				this.$router.push({name:'Home'})
            }
            console.warn(result)
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
};
</script>