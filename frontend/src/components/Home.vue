<template>
    <h4>Hello {{name}} ! Welcome to the Homepage.</h4>
    <p align="right" style="margin-right:20px">
     <router-link to="/add"><b style="color:black; font-family: Trebuchet MS, Tahoma, sans-serif;">Add Restaurant</b></router-link>
     <button style="margin-left:10px" @click="logout" type="submit" class="btn btn-dark">Logout</button>
    </p>
  <div v-if="restaurants.length != 0">
  <table class="table table-hover">
  <thead>
    <tr>
      <th scope="col">Id</th>
      <th scope="col">Name</th>
      <th scope="col">Address</th>
      <th scope="col">Contact</th>
      <th scope="col">Action</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="item in restaurants" :key="item.id">
      <th scope="row">{{item.id}}</th>
      <td>{{item.name}}</td>
      <td>{{item.address}}</td>
      <td>{{item.contact}}</td>
      <td><router-link :to="/update/+item.id"><b style = "color:dimgrey;">Update</b></router-link><button style="margin-left:5px" @click="deleteRes(item.id)" type="submit" class="btn btn-dark">Delete</button></td>
    </tr>
  </tbody>
  </table>
  </div>
  <div v-else><h2>Restaurant Data not available. Use <b>Add Restaurant</b> to add.</h2></div>
</template>

<script>
import axios from 'axios'
export default {
   name: "Home",
   data(){
    return{
        name:"",
        restaurants:[]
    }
   },
   methods:{
    logout(){
        localStorage.clear()
        this.$router.push({name:"LoginFile"})
    },
    async deleteRes(id){
      let result = await axios.delete("http://localhost:3000/res/"+id);
      if (result.status == 200){
        alert("Deleted Successfully");
        this.loadData();
      }
    },
    async loadData(){
       let user = localStorage.getItem('user-info');
        if (!user){
            this.$router.push({name:'LoginFile'})
        }
        this.name = JSON.parse(user).name
        let result = await axios.get("http://localhost:3000/res");
        this.restaurants=result.data; 
    }
   },
   mounted(){
      this.loadData();
    }
}
</script>


