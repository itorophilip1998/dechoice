<template>
  <div class="bg-light vh-100">
  <Loader v-if='loader'/>
    <Header :info="info"/>
      <div class="databox ">
        <form class="mt-5 pt-2 p-3" @submit.prevent="login()">
            <input type="email" v-model="details.email" required class="w-100 mt-4 p-2" placeholder="Email">

            <input required type="password" v-model="details.password" class="w-100 mt-4 mb-1 p-2" placeholder="Password" ref="password">
          <i v-if="!passwordCheckData" class="fa fa-eye link password-check  text-primary" @click="passwordCheck('show')" ></i>
           <i  v-if="passwordCheckData"  class="fa fa-eye-slash password-check  link text-primary" @click="passwordCheck('open')" ></i>
            <button  class="btn-success shadow w-100 mt-5 btn rounded-pill p-2">Login</button>
            <button class="bg-white shadow w-100 mt-3 btn rounded-pill p-2" type="button" @click="$router.push('/signup')">I don't have an account <b class="text-success">Signup</b></button>


     </form>
      </div>
  </div>
</template>


<script>
import Header from '@/components/auth-header'
import Loader from './Loader'
export default {
  components:{
    Header,
    Loader
  },
  data() {
    return {
    passwordCheckData:false,
    loader:false,
      info:{
          name:"Login",
          short_name:"Welcome Back!",
          details:"Login your account to access your details.",
          icon:"fa-sign-in",
          dashboard:false,
      },
      loader:false,
      details:{
        email:"",
        password:""
      }
    }
  },
  created(){
        localStorage.clear()
  },
  methods: {
   passwordCheck(data){
             if (data=="show") {
                 this.passwordCheckData=!this.passwordCheckData;
                 this.$refs.password.type="text"
             }
             else{
                this.passwordCheckData=!this.passwordCheckData;
                this.$refs.password.type="password"

             }
        },
        login(){ 
          this.loader=true
          this.$axios.post('/signin',this.details).then((result) => {
          this.loader=false
          localStorage.setItem('token',result.data.access_token)
          localStorage.setItem('user_id',result.data.user._id)
          localStorage.setItem('name',result.data.user.name)
          localStorage.setItem('email',result.data.user.email)
          
            this.$router.push("/dashboard")
            if(res.data.message="user Already exist") this.$router.push("/dashboard")
          }).catch((err) => {
          this.loader=false
          });
        }
},

}
</script>
<style >
.vh-100{
  height:100vh;
}

i.fa-eye-slash,i.fa-eye{
  position:absolute;
  right:30px;
  margin-top:-32px;
}

</style>

