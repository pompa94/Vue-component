<template>
<header>
    <h3>제품카테고리</h3>
    <dl>
        <dt>구매상품 총</dt>
        <dd>{{cartTotal}}원</dd>
        <dd>
            <button @click="displayCart = !displayCart">장바구니 보기 {{cart.length}} 개</button>
            <ul v-if="displayCart">
                <li v-for="(item,index) in cart" :key="index">
                    <span>
                        <img :src="item.image" :alt="item.name">
                    </span>
                    <span>{{item.name}} : {{item.price}} 원</span>
                </li>
            </ul>
        </dd>
        <dd></dd>
    </dl>
</header>
</template>


<script>
export default {
  data(){
    return{
        displayCart:false
    }
  },
  props:['cart'],
  computed:{
    cartTotal(){
        return this.cart.reduce((inc,item)=>Number(item.price)+inc, 0)
    }
  }
}
</script>


<style scoped>
header{
    display: flex;
    justify-content: flex-end;
    align-items: center;
    position: relative;
    padding: 10px 20px;
    border-bottom: 1px solid #666;
}
header>dl{
    display: flex;
    justify-content: flex-end;
    align-items: center;
}
header>dl>dd{}
header>dl>dd>ul{
    position: absolute;
    right: 0; top: 45px;
    z-index: 100;
    padding: 5px 10px ;
    border: 1px solid #666;
    background-color: #fff;
}
header>dl>dd>ul>li{
    border-bottom: 1px dotted #666;
    padding: 10px 0;
    display: flex;
    align-items: center;
}

header>dl>dd>ul>li>span:first-child>img{
    width: 50px;
    margin-right: 20px;
}
header>dl>dd>ul>li>span:last-child{
    color: green;
}

header>dl>dd>ul>li:last-child{
    border-bottom: none;
}
</style>