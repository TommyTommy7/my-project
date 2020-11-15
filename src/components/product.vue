<template>
    <div class="item">
    <!-- 概要のまとめ -->
    <figure class="image">
        <!-- セール対象なら -->
        <template v-if="product.isSale">
            <div class="status">SALE</div>
        </template>
        <!-- 画像データパスをバインド -->
        <img v-bind:src="product.image" alt="">
        <figcaption v-html="product.name"></figcaption>
    </figure>
    <!-- 価格詳細 -->
    <div class="detail">
        <!-- マスタッシュで価格データをバインド -->
        <div class="price"><span>{{product.price | number_format}}</span>円（税込）</div>
        <!-- 送料の表示 -->
        <!-- 0なら無料 -->
        <template v-if="product.delv === 0">
            <div class="shipping-fee none">送料無料</div>
        </template>
        <!-- 0でなければマスタッシュで送料表示 -->
        <template v-else>
            <div class="shipping-fee">+送料{{product.delv | number_format}}円</div>
        </template>
    </div>
    </div><!-- /.item-->
</template>

<script>
import './filter.js';

export default {
    name: 'Product',
    props: ['product'],
}
</script>

<style scoped>
/* 商品の各アイテム */
.item {
    flex: 0 1 250px;    /* flex-grow(伸び率):0 / flex-shrink(縮率):1 / flex-basis(幅):250px */
    margin-bottom: 30px;
}
.item .image {          /* itemクラス内のimageクラス */
    position: relative; /* ボックスの配置位置を他の位置要素を基準に相対配置 */
    text-align: center; /* 表示位置をセンタリング */
}
.item .image img {      /* imageクラス内の画像 */
    width: 100%;        /* 幅は100% */
    height: auto;       /* 高さは自動調整 */
}
.item .status {         /* itemクラス内のstatusクラス(SALEの表示)*/
    position: absolute; /* 表示位置は絶対位置指定(親要素の左上位置基準)⇒次の要素(画像)と重なる */
    border-radius: 50%; /* 四隅を丸く(=50%なので○の背景になる) */
    width: 4em;
    height: 4em;
    font-size: 12px;
    display: flex;
    align-items: center;    /* 内部を縦方向にセンタリング */
    justify-content: center;    /* 内部を横方向にセンタリング */
    background: #bf0000;    /* 背景色を赤*/
    color: #fff;            /* 文字色 */
}
.item .detail {         /* itemクラス内のdetailクラス(価格と送料) */
    text-align: center;     /* 文字をセンタリング */
}
.item .price {          /* itemクラス内のpriceクラス */
    display: inline-block;  /* ボックス型で表示 */
}
.item .price span {     /* priceクラス内のspan */
    font-size: 180%;    /* ちょっと大きめ表示 */
}
.item .shipping-fee {   /* itemクラス内のshipping-feeクラス */
    display: inline-block;  /* ボックス型で表示 */
    background: #f7cd12;    /* 背景色 */
    color: #000;            /* 文字色 */
}
.item .shipping-fee.none { /* itemクラス内のshipping-fee & none クラス */
    background: #bf0000;
    color: #fff;
}
</style>