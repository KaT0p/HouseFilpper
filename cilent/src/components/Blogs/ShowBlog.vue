<template>
    <div class="sb">
        <h1> ดูรายละเอียดงาน </h1>
            <p>id: {{ blog.id }} </p>
            <p>ชื่อผู้จ้าง : {{ blog.title }} </p>
            <p>ที่อยู่และติดต่อกลับ : {{ blog.content }} </p>
            <p>สถานที่ : {{ blog.category }} </p>
            <p>วันนัดทำความสะอาด : {{ blog.status }} </p>
            <b-button-group><p>
                <b-button v-on:click="navigateTo('/blog/edit/'+blog.id)"> แก้ไข </b-button>
                <b-button v-on:click="navigateTo('/blogs')"> กลับ </b-button>
            </p></b-button-group>
    </div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
    data () {
        return { 
            blog: null
        }
    },
    async created () {
        try {
            let blogId = this.$route.params.blogId
            this.blog = (await BlogsService.show(blogId)).data
        } catch (error) {
            console.log (error)
        }
    },
    methods: {
       navigateTo (route) {
           this.$router.push(route)
       },
    }
}
</script>
<style scoped>
.sb {
        margin-left: 10px;
        margin-top: 10px;
        margin-right: 10px;
    }
</style>
