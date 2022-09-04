<template>
  <div class="mcontaner">
    <Header></Header>

    <div class="block">
      <el-timeline>

        <el-timeline-item :timestamp="blog.created" placement="top" v-for="blog in blogs">
          <el-card class="el-card01">
            <h4>
              <router-link :to="{name: 'BlogDetail', params: {blogId: blog.id}}">
                {{blog.title}}
              </router-link>
            </h4>
            <p>{{blog.description}}</p>
          </el-card>
        </el-timeline-item>

      </el-timeline>

      <el-pagination class="mpage"
                     background
                     layout="prev, pager, next"
                     :current-page="currentPage"
                     :page-size="pageSize"
                     :total="total"
                     @current-change=page>
      </el-pagination>

    </div>

  </div>
</template>

<script>
  import Header from "../components/Header";

  export default {
    name: "Blogs.vue",
    components: {Header},
    data() {
      return {
        blogs: {},
        currentPage: 1,
        total: 0,
        pageSize: 5
      }
    },
    methods: {
      page(currentPage) {
        const _this = this
        _this.$axios.get("/blogs?currentPage=" + currentPage).then(res => {
          console.log(res)
          _this.blogs = res.data.data.records
          _this.currentPage = res.data.data.current
          _this.total = res.data.data.total
          _this.pageSize = res.data.data.size

        })
      }
    },
    created() {
      this.page(1)
    }
  }
</script>
<style>

	 .el-timeline-item__timestamp.is-top{
		color: #fff;
  }
	.el-card01{
		background: url(../images/bd740bcbbc06c8e71a4b9118684374f3.jpg);
		background-size: cover;
		opacity: 0.8
	}
	h4{
		z-index: 4;
	}
	.img{
		
		z-index: 1
	}
</style>
<style scoped>

  .mpage {
    margin: 0 auto;
    text-align: center;
  }
  .el-timeline-item__timestamp.is-top{
	color: #fff;
  }
  el-image{
	z-index: -1;
	background-size: cover;
  }
	.el-card__body{

	}
</style>