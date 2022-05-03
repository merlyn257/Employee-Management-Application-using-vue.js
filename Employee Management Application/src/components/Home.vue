<template>
    <div class="bg-red-900 my-0 py-10 shadow-xl">
        <h1 class="text-white font-bold text-3xl">EMPLOYEE MANAGEMENT SYSTEM</h1>
    </div>
<Header />
<div class="text-blue-900 mt-8">
    <div class="font-bold">
        <h1 class="text-3xl font-serif text-red-900">Hi {{name}}!</h1>
    </div>

    <div class="my-12 font-sans font-bold">
        <h2 class="text-3xl py-4">View Employees</h2>
        <table border="1" align="center" class="rounded-xl text-red-900">
            <tr class="bg-blue-200 text-xs fill-sky-100 grid-cols-6 shadow-md">
                <th class="px-10 py-2 font-bold">ID</th>
                <th class="px-10 font-bold">NAME</th>
                <th class="px-10 font-bold">AGE</th>
                <th class="px-10 font-bold">EMAIL</th>
                <th class="px-10 font-bold">CONTACT</th>
                <th class="px-10 font-bold">ADDRESS</th>
				<th class="px-8 font-bold">ACTIONS</th>
            </tr>
            <tr v-for="item in employee" :key="item.id" class="shadow-md">
                <td class="px-8 py-1.5 font-semibold">{{item.id}}</td>
                <td class="px-8 font-semibold">{{item.name}}</td>
                <td class="px-8 font-semibold">{{item.age}}</td>
                <td class="px-8 font-semibold">{{item.email}}</td>
                <td class="px-8 font-semibold">{{item.contact}}</td>
                <td class="px-8 font-semibold">{{item.address}}</td>
                <td class="px-8 font-semibold text-purple-500"><router-link :to="'/update/'+item.id">Update</router-link>
                    <button v-on:click="deleteEmployee(item.id)" class="px-8 font-semibold text-purple-500">Delete</button>
                </td>
            </tr>
        </table>
    </div>
</div>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios';
export default{
    name:'Home',
    data(){
        return{
            name:'',
            employee:[],
        }
    },
    components:{
        Header
    },
    methods:{
        async deleteEmployee(id)
        {
            let result = await axios.delete("http://localhost:3000/employee/"+id);
            console.warn(result)
            if(result.status==200)
            {
                this.loadData();
            }
        },
        async loadData()
        {
            let user=localStorage.getItem('user-info');
            this.name=JSON.parse(user).name;
            if(!user)
            {
                this.$router.push({name:'SignUp'})
            }
            let result = await axios.get("http://localhost:3000/employee");
            console.warn(result)
            this.employee=result.data;
        }
    },
    async mounted()
    {
        this.loadData();
    }
}
</script>