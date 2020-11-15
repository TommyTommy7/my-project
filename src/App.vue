<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <!-- 6-3のmain.htmlから移植 -->
    <!-- 商品一覧コンポーネント -->
    <product-list v-bind:products="products"></product-list>
  </div>
</template>

<script>
// HelloWorld.vue => prodcut-list.vueに変更
// import HelloWorld from './components/HelloWorld.vue'
import productList from './components/product-list.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld
    'product-list': productList
  },
  data: function() {
    return {
      // 商品リストを集めた商品リスト配列
      products:       [
          // id  名称                        価格         画像パス                送料    セール 
          {id:1, name:'Michel<br>スマホケース', price:1580, image:require('./assets/images/01.jpg'), delv:0, isSale:true},
          {id:2, name:'Raphael<br>スマホケース', price:1580, image:require('./assets/images/02.jpg'), delv:0, isSale:true},
          {id:3, name:'Gabriel<br>スマホケース', price:1580, image:require('./assets/images/03.jpg'), delv:240, isSale:true},
          {id:4, name:'Uriel<br>スマホケース', price:980, image:require('./assets/images/04.jpg'), delv:0, isSale:true},
          {id:5, name:'Ariel<br>スマホケース', price:980, image:require('./assets/images/05.jpg'), delv:0, isSale:false},
          {id:6, name:'Azrael<br>スマホケース', price:1580, image:require('./assets/images/06.jpg'), delv:0, isSale:false},
      ],
    }
  },
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
/* main.cssから移植 */
/* ベースのbody背景と文字色 */
body {
    background: #000;
    color: #fff;
}
/* セレクトボックス for 並び替えのセレクト */
select {
    background-color: #fff; /* 背景色を白 */
    border-radius: 5%;      /* 角を少し丸くする */
}
</style>
