<template>
  <div>
      <div class="search">
      <form class="form-inline my-2 my-lg-0 ">
        <input
          class="form-control mr-sm-2"
          type="search"
          placeholder="Search"
          aria-label="Search"
       v-model="search" />
        <button class="btn btn-outline-success my-2 my-sm-0" type="submit">
          Search
        </button>
      </form>
      </div>
      {{getCard()}}
    <div class="container" id="cont">
      <div class="row">
        <div class="col-sm" v-for="(c,i) in filteredTitles" v-bind:key="i">
          <h3>#{{ c.title}}-Resim</h3>
          <img v-bind:src="c.img" class="img" /><br/>
          
         <span>{{c.info}}</span>
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
export default {
  data() {
    return {
      posts: [],
      infos: [],
      titles:[],
      cart:[],
      search:'',
    };
  },

  methods: {
    async getData() {
      try {
        let response = await fetch(
          "https://api.unsplash.com/photos/?client_id=-wSoIKs6oTZ7A6LwhNEtWr5A1sJo6RPf7S_JrZ2eGY8"
        );
        this.posts = await response.json();
        
      }catch (error) {
        console.log(error);
      }
    },
    async getInfo() {
      try {
        let res = await fetch(
          "https://jsonplaceholder.typicode.com/posts"
        );
        this.infos = await res.json();
        
        
        
      }catch (error) {
        console.log(error);
      }
    },
     getTitle(){
      let a=Math.floor(1000 + Math.random() * 9000).toString()
    this.titles.push(a)
   return a
   
    },
    getCard(){
      for(var i=0;i<this.posts.length;i++){
       let b ={
          title:this.getTitle(),
          img:this.posts[i].urls.raw,
          info:this.infos[i].title
        }
        this.cart.push(b)
        console.log(this.cart)
        
      }
    }

  
 },

  created() {
    this.getData();
    
    this.getInfo();
    this.getTitle();
    this.getCard();
  },
  computed:{
  filteredTitles:function(){
    return this.cart.filter((item)=>{
     return item.title.match(this.search)
    })
  }
  }
}
</script>

<style>
.img {
  height: 300px;
  width: 300px;
  margin-top: 20px;
}
#cont {
  margin-top: 50px;
  text-align: center;
}
.search{
  margin-left: 50%;
}
</style>
