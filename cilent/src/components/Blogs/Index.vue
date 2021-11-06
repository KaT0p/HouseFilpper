<template>
    <div class="blogs">
        <h2> งานทั้งหมด </h2>

        <!-- <p><button v-on:click="logout"> Logout </button></p> -->

        <hr/><h4> รายการทำความสะอาด {{blogs.length}}</h4>
        <b-button-group><p>
            <b-button variant="success" v-on:click="navigateTo('/blog/create')"> Create work </b-button>
        </p></b-button-group>
        <div v-for="blog in blogs" v-bind:key="blog.id">
            <!--<p>id: {{ blog.id }} </p>-->
            <p>ชื่อผู้จ้าง: {{ blog.title }} </p>
            <p>ที่อยู่และติดต่อกลับ : {{ blog.content }} </p>
            <p>สถานที่ : {{ blog.category }} </p>
            <p>วันนัดทำความสะอาด: {{ blog.status }} </p>
            <b-button-group><p>
                <b-button v-on:click="navigateTo('/blog/'+ blog.id)"> ดูรายละเอียดงาน</b-button>
                <b-button v-on:click="navigateTo('/blog/edit/'+ blog.id)"> แก้ไขงาน </b-button>
                <b-button v-on:click="deleteBlog(blog)"> ลบงาน </b-button>
            </p></b-button-group>
            <hr>
        </div>
    </div>
</template>
<script>
import BlogsService from '@/services/BlogsService'
export default {
    data () {
        return { 
            blogs: []
        }
    },
    async created () {
        this.blogs = (await BlogsService.index()).data
    },
    methods: {
       /*  logout () {
            this.$store.dispatch('setToken', null)
            this.$store.dispatch('setBlog', null)
            this.$router.push({
                name: 'login'
            })
        }, */
        navigateTo (route) {
            this.$router.push(route)
        },
        async deleteBlog (blog) {
            let result = confirm("Want to delete?")
            if (result) {
                try {
                    await BlogsService.delete(blog)
                    this.refreshData()
                } catch (err) {
                    console.log(err)
                }
            }
        },
        async refreshData() {
            this.blogs = (await BlogsService.index()).data
        }
    }
}
</script>
<style scoped>
    .blogs {
        margin-left: 10px;
        margin-top: 10px;
        margin-right: 10px;
    }
</style>
