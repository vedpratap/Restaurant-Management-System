<template>
      <div class="card m-auto" style="width: 22rem;">
        <!--img src ="/static/imgs/banner.png"-->
        <div class="card-header">
            <h2>Sign Up</h2>
        </div>
        <div class="card-body">
            <div class="form-group">
                <label for="name"><b>Full Name</b></label>
                <input
                    type="text"
                    class="form-control"
                    v-model="name"
                    id="name"
                    name="name"
                    placeholder="Enter your full name"
                    maxlength="30"
                    style="width: 300px;text-align: center"
                    required/>
            </div>
            <div class="form-group">
              <label for="email"><b>Email address</b></label>
              <input type="email" class="form-control" v-model="email" id="email" name="email" aria-describedby="emailHelp" placeholder="Enter email">
              <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
            </div>
            <!--div class="form-group">
              <label style="padding-top: 10px" for="city"><b>City</b></label>
                <select style="width: 300px;text-align: center" id="city"  class="form-control"  name="city" required>
                  <option value="Patna">Patna</option>
                  <option value="Mumbai">Mumbai</option>
                  <option value="Pune">Pune</option>
                  <option value="Bengaluru">Bengaluru</option>
                  <option value="Delhi">Delhi</option>
                  <option value="Hyderabad">Hyderabad</option>
                  <option value="Ahmedabad">Ahmedabad</option>
                  <option value="Chennai">Chennai</option>
                  <option value="Kolkata">Kolkata</option>
                  <option value="Surat">Surat</option>
                  <option value="Jaipur">Jaipur</option>
                  <option value="Lucknow">Lucknow</option>
                  <option value="Kanpur">Kanpur</option>
                  <option value="Nagpur">Nagpur</option>
                  <option value="Indore">Indore</option>
                  <option value="Thane">Thane</option>
                  <option value="Madurai">Madurai</option>
                </select>
            </div-->
            <div class="form-group">
              <label for="password"><b>Password</b></label>
              <input type="password" v-model="password" class="form-control" id="password" name = "password" placeholder="Password">
            </div>
            <p>Have an account? <router-link to="/login"><b style = "color:dimgrey;">Login</b></router-link></p>
            <button @click="signup" type="submit" class="btn btn-dark">Submit</button>
        </div>
      </div>
</template>

<script>
import axios from 'axios'
export default {
   name: 'SignUp',
   date(){
    return{
      name:"",
      email:"",
      password:""
    }
   },
   methods:{
    async signup(){
      let result = await axios.post("http://localhost:3000/user",{
        name:this.name,
        email:this.email,
        password:this.password
      })
      .catch(e => {
      console.error(e);
       });
      if(result.status == 201){
        alert("Sign Up Successfuly.")
        this.$router.push({name:'LoginFile'})
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