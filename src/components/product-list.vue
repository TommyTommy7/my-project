<template>
    <div class="container">
        <!-- ヘッダーコンポーネント(検索や並び替え、件数) -->
        <product-header
            v-bind:count="filteredList.length"
            v-bind:showSaleItem="showSaleItem"
            v-bind:showDelvFree="showDelvFree"
            v-bind:sortOrder="sortOrder"
            v-on:showSaleItemChanged="showSaleItem = !showSaleItem"
            v-on:showDelvFreeChanged="showDelvFree = !showDelvFree"
            v-on:sortOrderChanged="sortOrderChanged"
        >
        </product-header>
        <!-- 商品のリスト -->
        <div class="list">
            <!-- v-forで絞り込まれたfilteredList分を商品コンポーネントに割り当てて行く -->
            <product
                v-for="product in filteredList"
                v-bind:product="product"
                v-bind:key="product.id"
            ></product>
        </div><!-- /.list -->
    </div><!-- /.container-->
</template>

<script>
import productHeader from './product-header';
import product from './product.vue';

export default {
    name: 'ProductList',    // コンポーネント名
    props: ['products'],    // 親の商品データを参照
    // 子コンポーネントをローカルスコープで定義
    components: {
        'product-header': productHeader,    // ヘッダーコンポーネント
        'product': product,                 // 商品コンポーネント
    },
    // データ
    data: function() {
        return {
            showSaleItem:   false,  // 検索条件「セール対象」チェック状態
            showDelvFree:   false,  // 検索条件「送料無料」チェック状態
            sortOrder:      1,      // 「並び替え」の選択値(1:標準 2:価格が安い順)
        }
    },
    // メソッド
    methods: {
        // sortOrdeChangedカスタムイベントで呼ばれるメソッド
        // 「並び替え」セレクトの選択値が変わった時の処理
        sortOrderChanged: function(order) {
            this.sortOrder = order; // 引数で取得したセレクト値を自分のsortOrderプロパティにコピー
        }
    },
    // 算出プロパティ
    computed: {
        // 現在の検索条件を元に絞り込んだ商品リストを返す算出プロパティ
        filteredList: function() {
            let newList = [];   // 絞り込み後のリスト格納用排列初期化準備
            for (let i=0; i<this.products.length; i++) {
                let isShow = true;
                if ( (this.showSaleItem && !this.products[i].isSale) ||     // セール対象チェックON & セール対象でない
                    (this.showDelvFree && this.products[i].delv) > 0 ){    // 又は送料無料チェックON & 送料あり
                    isShow = false; // いずれかの条件に当てはまったものは表示しない
                }
                // 表示対象だった商品だけ、絞り込み後のリストに格納する
                if (isShow) {
                    newList.push(this.products[i]);
                }
            }
            // 並び替えの選択に従って絞り込み後の排列を並び替える
            if (this.sortOrder === 1){      // 標準
                // 並び替える必要なし
            }
            else if (this.sortOrder == 2) { // 価格が安い順
                newList.sort(function(a,b){
                    return a.price - b.price;
                });
            }
            // 絞り込み後のリストを返す
            return newList;    
        }
    },
}
</script>

<style scoped>
/* 全体をラップするcontainerクラス */
.container {
    width: 960px;       /* 横幅960pxで固定 */
    margin: 0 auto;     /* 外枠の設定:上下はなし 左右は自動 */
}

/* 商品一覧をまとめるlistクラス */
.list {
    display: flex;      /* フレックスボックスにして小アイテムを横並びにする */
    flex-wrap: wrap;    /* 小アイテムを内側にラップして左上から並べる */
    justify-content: space-between; /* 等間隔に並べる */
}
.list::after {          /* listクラスのすぐ後ろに含めるコンテンツ */
    content: "";        /* 取り敢えず空 */
    display: block;     /* ボックス型で表示 */
    width: 250px;       /* 幅だけ指定 */
}
</style>