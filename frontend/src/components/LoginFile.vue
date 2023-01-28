<template>
        <div class="card m-auto" style="width: 22rem;">
          <!--img src ="/static/imgs/banner.png"-->
          <div class="card-header" id = "heading">
              <h2>Login</h2>
          </div>
          <div class="card-body">
              <div class="form-group">
                <label for="email"><b>Username</b></label>
                <input type="email" v-model="email" class="form-control" id="email" name = "email" aria-describedby="emailHelp" placeholder="Enter email">
                <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
              </div>
              <div class="form-group">
                <label for="password"><b>Password</b></label>
                <input  type="password" v-model="password" class="form-control" id="password" name = "password" placeholder="Password">
              </div>
              <p>Didn't have an account?<router-link to="/signup"><b style = "color:dimgrey;">Sign Up</b></router-link></p>
              <button @click="login" type="submit" class="btn btn-dark">Submit</button>
          </div>
        </div>
</template>

<script>
import axios from 'axios'
export default{
    name: 'LoginFile',
    data(){
      return{
        email:"",
        password:""
      }
    },
    methods:{
      async login(){
        let result = await axios.get(`http://localhost:3000/user?email=${this.email}&password=${this.password}`
        );
        if (result.status == 200 && result.data.length > 0){
          localStorage.setItem("user-info", JSON.stringify(result.data[0]));
          this.$router.push({name:"Home"});
        }
        else{
          alert("User not found!!");
        }
      }
    },
    mounted(){
        let user = localStorage.getItem('user-info');
        if (user){
            alert("You have already logged in! Please Logout First.")
            this.$router.push({name:"Home"});
        }
    }
}
</script>

<style scoped>
</style>
