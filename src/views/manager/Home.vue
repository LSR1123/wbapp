<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
    </header>
  <div>

    <!-- 分类6个 -->
  <van-grid :column-num="3">
  <van-grid-item
    v-for="value in categories"
    :key="value.id"
    :icon="value.icon"
    :text="value.name"
  />
  </van-grid>
    <!-- 产品 6个 -->
  <van-grid :column-num="1" icon-size="400px">
  <van-grid-item
    v-for="value in products"
    :key="value.id"
    :icon="value.icon"
    :text="value.name"
  />
</van-grid>
  </div>
  </div>
</template>
<script>
import {get,post} from '../../http/axios';
import {mapState, mapActions} from 'vuex'
export default { 
  data(){
    return{
      categories:{},
      products:{}
    }
  },
  created(){
    this.LoadCategory();
    this.loadProduct();
  },
  methods:{
    LoadCategory(){
      let url = "/category/findAll";
      get(url).then((response)=>{
        this.categories = response.data.slice(0,6);
      })
    }
  },
  loadProduct(){
    let url = "/product/query"
    let param = {
      page : 0,
      pageSize :10
    }
    post(url,params).then ((response)=>{
      this.product = response.data.list;
    })
  },
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>