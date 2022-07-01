<template>
    <div>
        <figure>
            <img 
                :src="item.image" 
                :alt="item.name" />
            <figcaption>
                <dl>
                    <dt><!-- 이름 -->
                    {{item.name}}</dt>
                    <dd><!-- 설명 -->
                        {{item.description}}
                    </dd>
                    <dd>
                        <span v-if="item.price > 15000 && displayLabel" class="blue">premier
                        </span>
                        <span  v-else-if="(item.price <= 15000 && item.price > 10000) && displayLabel" class="green">value
                        </span>
                        <span v-else-if="item.price <= 10000 && displayLabel" class="orange">sale
                        </span>
                    </dd>
                    <dd>가격
                        {{item.price}}
                    </dd>
                </dl>
            </figcaption>
        </figure>
        <p>
            <button @click="$emit('addToCart',item)">+</button>
        </p>
    </div>
</template>


<script>
export default {
  props:{
    item:{type:Object}
  },
  emits:['addToCart'],
  displayLabel:true
}
</script>


<style scoped>
figure{
    width: 800px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-content: flex-start;
}
figure>img{
    width: 150px;
}
figure>figcaption{
    width: 500px;
    /* background-color: rgb(252, 237, 240); */
}

figure dl{
    padding: 0 20px;
}
figure dl>dt{
    font-size: 1.5em;
    padding: 8px 0;
    border-bottom: 1px dotted #666;
}
figure dl>dd{
    padding: 5px 0;
    border-bottom: 1px dotted #666;
}
figure dl>dd:last-child{
    border-bottom: none;
}
figure dl>dd:nth-of-type(2){
    padding: 10px 0;
    text-align: right;
}
figure dl>dd>span{
    color: #fff;
    line-height: 35px;
    padding: 0 10px;
    border-radius: 4px;
    display: inline-block;
}
figure dl>dd>span.blue{
    background-color: rgb(42, 42, 190);
}
figure dl>dd>span.green{
    background-color: rgb(96, 226, 96);
}
figure dl>dd>span.orange{
    background-color: rgb(207, 153, 51);
}

p{
    width: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
}
</style>