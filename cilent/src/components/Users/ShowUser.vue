<template>
    <div class="SU">
        <h1>Show User</h1>
        <p>ID : {{ user.id }} </p>
        <p>ชื่อ - นามสกุล {{user.name}} - {{user.lastname}}</p>
        <p>Email : {{user.email}} </p>
        <p>Password : {{user.password}}</p>
        <b-button-group><p>
                <b-button v-on:click="navigateTo('/users')"> กลับ </b-button>
        </p></b-button-group>
    </div>
</template>
<script>
import UsersService from '@/services/UsersService'
export default {
    data() {
        return {
            user: null,
        };
    },
    methods: {
        navigateTo(route) {
        console.log(route);
        this.$router.push(route);
        },
    },
    async created() {
        try {
            let userId = this.$route.params.userId;
            this.user = (await UsersService.show(userId)).data
        } catch (error) {
            console.log(error);
        }
    },
    methods:{
        navigateTo(route){
            this.$router.push(route)
        },
    },
};
</script>
<style scoped>
    .SU {
        margin-left: 10px;
        margin-top: 10px;
        margin-right: 10px;
    }
</style>
