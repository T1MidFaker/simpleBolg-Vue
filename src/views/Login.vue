<template>
 <div class="bg001" style="background: url(../images/wallhaven-dpvykm.jpg)">
	 <div class="bg01">
    <el-container class="el-c">
      <el-header class="u1">
	     欢迎登录Hirohima的个人博客
      </el-header>
      <el-main class="e-m">
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm aaa">
          <el-form-item label="用户名" prop="username">
            <el-input v-model="ruleForm.username"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="password">
            <el-input type="password" v-model="ruleForm.password"></el-input>
          </el-form-item>

          <el-form-item>
            <el-button type="primary" @click="submitForm('ruleForm')">登录</el-button>
            <el-button @click="resetForm('ruleForm')">重置</el-button>
          </el-form-item>
        </el-form>

      </el-main>
    </el-container>

  </div>
 </div>
</template>

<script>
  export default {
    name: "Login",
    data() {
      return {
        ruleForm: {
          username: '',
          password: ''
        },
        rules: {
          username: [
            { required: true, message: '请输入用户名', trigger: 'blur' },
            { min: 3, max: 15, message: '长度在 3 到 15 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请选择密码', trigger: 'change' }
          ]
        }
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            const _this = this
            this.$axios.post('/login', this.ruleForm).then(res => {

              console.log(res.data)
              const jwt = res.headers['authorization']
              const userInfo = res.data.data

              // 把数据共享出去
              _this.$store.commit("SET_TOKEN", jwt)
              _this.$store.commit("SET_USERINFO", userInfo)

              // 获取
              console.log(_this.$store.getters.getUser)

              _this.$router.push("/blogs")
            })

          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      }
    }
  }
</script>
<style>
	html{
	height: 100%
	}
	body{
		width:100%;
		height:100%;
		margin:0px;
		padding:0px;
		background: url(../images/wallhaven-3z7k6y.jpg);
		background-size: 100% 100% ;
		
}
	.u1{
		color: #fff;
		font-size: 20px
	}
	
	
</style>
<style scoped>
	.el-form-item__label{
		color: #fff;
	}
	.bg001{
		background-color: '#FAEBD7'
	}
	body{
		background-color: '#FAEBD7'
	}
.el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
	margin-top: 100px;
	opacity: 0.6;
  }
	.e-m{
		
		background: url(../images/wallhaven-dpvykm.jpg);
		height: 320px;
		align-text: center;
		background-size: 100% 100%;
	}
  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
  }

  .el-main {
    /*background-color: #E9EEF3;*/
    color: #fff;
    text-align: center;
    line-height: 160px;
	opacity: 0.9
  }

  body > .el-container {
    margin-bottom: 40px;
  }

	.el-form-item{
		color: '#fff';
	}
  .mlogo {
    height: 60%;
    margin-top: 10px;
  }

  .demo-ruleForm {
    max-width: 500px;
    margin: 50px auto;
  }

</style>