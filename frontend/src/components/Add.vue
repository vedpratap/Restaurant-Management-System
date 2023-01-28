v<template>
      <div class="card m-auto" style="width: 22rem;">
        <!--img src ="/static/imgs/banner.png"-->
        <div class="card-header">
            <h2>Add Restaurant</h2>
        </div>
        <div class="card-body">
            <div class="form-group">
                <label for="name"><b>Name</b></label>
                <input
                    type="text"
                    class="form-control"
                    v-model="name"
                    id="name"
                    name="name"
                    placeholder="Enter Restaurant Name"
                    maxlength="100"
                    style="width: 300px;text-align: center"
                    required/>
                <label for="address"><b>Address</b></label>
                <input
                    type="text"
                    class="form-control"
                    v-model="address"
                    id="address"
                    name="address"
                    placeholder="Enter Address"
                    maxlength="500"
                    style="width: 300px;text-align: center"
                    required/>
                <label for="contact"><b>Contact</b></label>
                <input
                    type="text"
                    class="form-control"
                    v-model="contact"
                    id="contact"
                    name="contact"
                    placeholder="Enter Mobile Number"
                    maxlength="10"
                    style="width: 300px;text-align: center"
                    required/>
            </div>
            <p>Want to go to home? <router-link to="/"><b style = "color:dimgrey;">Click Here</b></router-link></p>
            <button @click="add" type="submit" class="btn btn-dark">Add Restaurant</button>
        </div>
      </div>
</template>

<script>
import axios from 'axios'
export default {
   name: 'Add',
   data(){
    return{
        name:"",
        address:"",
        contact:""
    }
    },
   methods:{
    async add(){
      let result = await axios.post("http://localhost:3000/res",{
        name:this.name,
        address:this.address,
        contact:this.contact
      })
      .catch(e => {
      console.error(e);
       });
      if(result.status == 201){
        alert("Added Successfuly.")
        this.$router.push({name:'Home'})
      }
    }
   },
    async  mounted(){
        let user = localStorage.getItem('user-info');
        if (!user){
            this.$router.push({name:'LoginFile'})
        }
    }
 
}
</script>