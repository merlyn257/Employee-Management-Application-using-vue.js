<template>
    <div class="nav grid-cols-3 py-2 text-red-900 font-bold shadow-lg">
        <router-link to="/">View &nbsp; &nbsp; &nbsp;</router-link>
        <router-link to="/add">Add &nbsp; &nbsp; &nbsp;</router-link>
        <!--<router-link to="./update">Update&nbsp; &nbsp; &nbsp;</router-link>-->
		<!--<router-link to="./delete">Delete&nbsp; &nbsp; &nbsp;</router-link>-->
        <a v-on:click="logout" href="#">Logout</a>
    </div>
</template>

<script>
export default {
    name: 'Header',
    methods:{
        logout()
        {
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>