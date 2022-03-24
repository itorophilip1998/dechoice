<template>
  <div>
    <Header :info="info"/>
  <Loader v-if='loader'/>

      <div class="databox pb-3">
        <form class="mt-5 py-2 p-3"  @submit.prevent="register()"> 
            <input type="email" v-model="details.email" required class="w-100 mt-4 p-2" placeholder="Email">

            <input required type="password" v-model="details.password" class="w-100 mt-4 mb-1 p-2" placeholder="Password" ref="password">
          <i v-if="!passwordCheckData" class="fa fa-eye link password-check  text-primary" @click="passwordCheck('show')" ></i>
           <i  v-if="passwordCheckData" class="fa fa-eye-slash password-check  link text-primary" @click="passwordCheck('open')" ></i>

            
            <button class="btn-success shadow w-100 mt-5 btn rounded-pill p-2">Signup</button>
            <button class="bg-white shadow w-100 mt-3 btn rounded-pill p-2" type="button" @click="$router.push('/login')">I have an account already <b class="text-success">Login</b> </button>


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
      loader:false,
    passwordCheckData:false,
      info:{
          name:"Register",
          short_name:"Create new account!",
          details:"Signup to  access your order",
          icon:"fa-pencil",
          dashboard:false,
      },
      details:{ 
        email:"",
        password:""
      }
    }
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
           register(){ 
          this.loader=true
          this.$axios.post('/signup',this.details).then((result) => {
          this.loader=false
          localStorage.setItem('token',this.result.access_token)
          localStorage.setItem('user_id',this.result.user._id) 
          localStorage.setItem('email',result.data.user.email) 
            this.$router.push("/dashboard")  
          }).catch((err) => {
          this.loader=false

            if(err.response.status==404){
                this.$router.push("/login")
            }
          });
        }
},

}
</script>
<style >

i.fa-eye-slash,i.fa-eye{
  position:absolute;
  right:30px;
  margin-top:-32px;
}

</style>

