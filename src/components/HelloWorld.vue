<template>
<!--  <div class="hello">-->
<!--    <h1>{{ msg }}</h1>-->
<!--    <p>-->
<!--      For a guide and recipes on how to configure / customize this project,<br>-->
<!--      check out the-->
<!--      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.-->
<!--    </p>-->
<!--    <h3>Installed CLI Plugins</h3>-->
<!--    <ul>-->
<!--      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-babel" target="_blank" rel="noopener">babel</a></li>-->
<!--      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-eslint" target="_blank" rel="noopener">eslint</a></li>-->
<!--    </ul>-->
<!--    <h3>Essential Links</h3>-->
<!--    <ul>-->
<!--      <li><a href="https://vuejs.org" target="_blank" rel="noopener">Core Docs</a></li>-->
<!--      <li><a href="https://forum.vuejs.org" target="_blank" rel="noopener">Forum</a></li>-->
<!--      <li><a href="https://chat.vuejs.org" target="_blank" rel="noopener">Community Chat</a></li>-->
<!--      <li><a href="https://twitter.com/vuejs" target="_blank" rel="noopener">Twitter</a></li>-->
<!--      <li><a href="https://news.vuejs.org" target="_blank" rel="noopener">News</a></li>-->
<!--    </ul>-->
<!--    <h3>Ecosystem</h3>-->
<!--    <ul>-->
<!--      <li><a href="https://router.vuejs.org" target="_blank" rel="noopener">vue-router</a></li>-->
<!--      <li><a href="https://vuex.vuejs.org" target="_blank" rel="noopener">vuex</a></li>-->
<!--      <li><a href="https://github.com/vuejs/vue-devtools#vue-devtools" target="_blank" rel="noopener">vue-devtools</a></li>-->
<!--      <li><a href="https://vue-loader.vuejs.org" target="_blank" rel="noopener">vue-loader</a></li>-->
<!--      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank" rel="noopener">awesome-vue</a></li>-->
<!--    </ul>-->
<!--  </div>-->
  <div class="div">
    <div>URL: {{ url }}</div>
    <div>TITLE: {{ title }}</div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      url: process.env.VUE_APP_URL,
      title: process.env.VUE_APP_TITLE,
      newProducts:[],
    }
  },
  props: {
    msg: String
  },

  methods:{
    fetchData(){
      // axios.get('https://jsonplaceholder.typicode.com/todos').then(response=>{
      //   console.log(response.data)
      //   this.branches=response.data
      //   console.table(this.branches)
      // })


      // axios.get(this.url+'api/branch').then(response=>{
      //   console.log(response.data.data)
      //   this.branches=response.data.data
      //   console.table(this.branches)
      // })

      let branchID=localStorage.branchID
      console.log(branchID)

      // axios.get(this.url+'/api/category/branch/' + branchID).then(response=>{
      //   console.log(response.data.info)
      //   //this.branches=response.data.data
      //   //console.table(this.branches)
      // })


      // axios.get('http://developer.amanabigbazar.com/api/category/branch/' + branchID).then(response=>{
      //   console.log(response.data.info)
      //   //this.branches=response.data.data
      //   //console.table(this.branches)
      // })




      setTimeout(()=>{
        console.log("Calling Get Special offer Product")
        // let requestLink=this.url+'api/product/search/list/1' + '?branch='+ localStorage.branchID

        //let requestLink='/api/product/search/list/1' + '?branch='+ localStorage.branchID
        let requestLink='http://developer.amanabigbazar.com/api/product/search/list/1' + '?branch='+ localStorage.branchID
        axios.post(requestLink, {
          category:null,
          subcategory:null,
          brand:null,
          supplier:null,
          name:null,
          min_price:null,
          max_price:1000000,
          new_product: false,
          special_offer: true
        }).then( response => {
          if (response.data.data.length) {
            console.log("Found New Product")
            this.newProducts=response.data.data
            console.log(this.newProducts)
          } else {
            console.log()
          }
        });
      },2000)
    },
  },

  mounted() {
    localStorage.setItem('branchID','5f82a8635e989e064902d02e')
    localStorage.setItem('userToken','eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7ImlkIjoiNjAzNTIwY2VkNzMzMTExNGRkMjU3OTYyIn0sImlhdCI6MTYxNDUxMzUxNywiZXhwIjoxNjE0ODczNTE3fQ.nnaOStkkjRIrCpICISgIVrtNzWfaFYwuqIOz9in8it0')
    this.fetchData()
    console.log(this.url)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
