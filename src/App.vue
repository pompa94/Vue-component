<template>
  <article>
    <!-- header -->
    <NavPrice :cart="cart" />
    <!-- div#box -->
    <div id="box">
      <ul class="form">
        <li>
          <span>
            <label for="userMax">최고값</label>
            <input id="userMax" v-model="max" readonly />
          </span>
          <span>
            선택상품 갯수 : {{filterProducts.length}}
          </span>
        </li>
        <li>
          <input type="range" min="0" max="30000" step="500" v-model="max" />
        </li>
        <li>
          <input type="checkbox" id="userLabel" v-model="displayLabel" />
          <label for="userLabel">레벨보기</label>
        </li>
      </ul>
      <ul class="list">
        <li v-for="(item,index) in filterProducts" :key="index">
          <ProductItem :item="item" :cart="cart" @addToCart="addToCart"  />
        </li>
      </ul>
    </div>
  </article>
</template>


<script>
import NavPrice from "@/components/NavPrice.vue";
import ProductItem from "@/components/ProductItem.vue";
import ProductData from '@/assets/data.json'
export default {
  data(){
    return {
      products:ProductData,
      displayCart:false,
      cart:[],
      displayLabel:true,
      max:20000
      }
  },
  components:{
    NavPrice,
    ProductItem
  },
  computed:{
    filterProducts(){
      return this.products.filter((item) => (item.price) < this.max)
    },
    cartTotal(){
      return this.cart.reduce((inc,item) => Number(item.price)+inc, 0)
    }
  },
  methods : {
    addToCart(product){
      this.cart.push(product)
    }
  }
}
</script>


<style scoped>
  
body{
    background-color: #666;
}

article{
    width: 1000px;
    margin: 0 auto;
    padding: 0 200px;
    background-color: #fff;
}

div#box{
}

div#box>ul.form{
    padding: 30px 0;
}
#box>ul.form>li{
    margin-bottom: 20px;
}
#box>ul.form input{
    border: none;
    font-size: 25px;
}
#box>ul.form input[type="range"]{
    width: 600px;
}
#box>ul.form label{
    display: inline;
    padding: 0 20px;
}

#box>ul.list{
    padding: 20px 30px;
}
#box>ul.list>li{
    padding: 5px 0;
    border: 1px dotted #666;
}
#box>ul.list>li>div{
    display: flex;
    flex-direction: row-reverse;
    flex-wrap: wrap;
    justify-content: space-between;
}
</style>