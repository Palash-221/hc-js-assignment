<template>
<div>
  <span class="filter">
    
  <div class="dropdown">
    <p>{{category}}</p>
    <span class="span"><p @click="sortbyr">Sort By:</p>
  <button class="dropbtn">Filter <i class="fa fa-angle-down" style="font-size:24px"></i>
</button></span> 
  <div class="dropdown-content">
  <a @click="sortbylow">Price :Low to High</a>
  <a @click="sortbyhigh">Price :High to Low</a>
   
  </div>
   
</div> <p>Products found:{{size}}</p></span>

  
<div class="item">

  <!--  -->
 <div class="cate">
   <h2>Category</h2>
     <router-link  class="category" to="/men">MEN</router-link>
       <router-link class="category"  to="/women">WOMEN</router-link>
         <router-link  class="category" to="/electronics">GREAR</router-link>
           <router-link  class="category" to="/jewelery">TRAINING</router-link>
   </div>
 <div v-for="item in items" :key="item"  >
  
<div class="card">
  <img :src="item.image" alt="" style="width:200px; height:300px">
    <router-link :to="{ name: 'product', params: { id: item.id } }"
        ><p>
          <b>{{ item.title }}</b>
        </p></router-link>

  <p class="price">${{item.price}}</p>

  <div class="star">
  <span class="fa fa-star checked"></span>
<span class="fa fa-star checked"></span>
<span class="fa fa-star checked"></span>
<span class="fa fa-star checked"></span>
<span class="fa fa-star checked"></span>


</div>

</div>


 </div>
</div>
</div>
</template>

<script>
import axios from "axios";
export default {
    name:'Category',
    props:['category'],
    data() {
        return {
            items:[],
            size:undefined,
        men:"men's clothing",
        women:"women's clothing"
      }
           
        
    },methods: {
      sortbylow(){
      this.items.sort((a,b)=>a.price<b.price?-1:1)
      console.log("sorted")
      },sortbyhigh(){
      this.items.sort((a,b)=>a.price<b.price?1:-1)
      console.log("sorted")
      },sortbyr(){
      this.items.sort((a,b)=>a.rating.rate<b.rating.rate?-1:1)
      console.log("sorted")
      }
    },
    mounted() {
        axios
          .get("https://fakestoreapi.com/products/category/"+this.category)
          .then((response) => {
    this.items=response.data;
    this.size=response.data.length;
    }); 
    //console.log(items);
  }
}
</script>
<style>
.span{
  display: flex;
  margin-left: 180px;
}
.checked{
  color:  #5ECE7B;
  display: flex;
  padding: 5px;
}
.star{
  display: flex;
  margin:auto;
}
.filter{display: flex;
align-items: center;
  text-align: center;
  justify-items: center;
  /* border: 2px solid black; */
  padding-right:20px; 
  box-shadow: 1px 1px 1px 2px gainsboro;
  height: 60px;
  
  justify-content: space-between
}
.dropdown{
  display: flex;
  margin-left:50px;
}
p{
  float: right;
  /* margin-top: -15px; */
  /* margin-right: 15px; */
   font-weight: 300;
    font-size: 18px;
  
    /* margin-left: 200px */
}
.cate{
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  padding: 10px;
  box-shadow: 1 px 1 px  grey;
 margin-right: 25px
}
select{
  margin-left:30px 
}
.category{
   color:black;
   font-weight: 300;
   font-size: 18px;
padding: 20px;
display: flex;
justify-content: flex-start;
}
.item{
  /* display: flex; */
  /* flex-wrap: wrap; */
  display: flex;
  /* flex-wrap: wrap; */
  /* border: 2px solid firebrick; */
  width: 90%;
  /* overflow: hidden; */
  
}.card{
/* width: 20%; */
padding: 30px;
margin: 10px;
}
.dropbtn {
  display: flex;
  /* color: black; */
  background-color: #ffff; 
  /* padding: 16px; */
  width: 80px;
  font-size: 19px;
  margin-top: -10px;
  padding-left:10px; 
  border: none;
  cursor: pointer;
  justify-content: space-between;
  align-items: center;
  /* margin-left: 200px */
}
.dropdown {
  position: relative;
  /* display: inline-block; */
  display: flex;
  align-items: center;
  justify-content: space-around;
}
.dropdown-content {
  display: none;
  position: absolute;
  background-color: #f9f9f9;
  min-width: 160px;
  box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
  margin-top:30px;
  z-index: 1;
  margin-left: 280px;
  margin-top:100px;
  cursor: pointer;
}
.dropdown-content a {
  color: black;
  padding: 12px 16px;
  text-decoration: none;
  display: block;
  
}
.dropdown-content a:hover {background-color: #f1f1f1}
.dropdown:hover .dropdown-content {
  display: block;
}

</style>
