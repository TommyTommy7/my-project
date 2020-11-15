<template>
    <header>
        <h1 class="pagetitle">商品一覧</h1>
        <!-- 検索欄 -->
        <div class="search">
            <div class="result">
                検索結果 <span class="count">{{count}}</span>
            </div><!-- /.result -->
            <!-- 表示条件設定 -->
            <div class="condition">
                <!-- 絞り込みチェックボックス -->
                <div class="target">
                    <label><input type="checkbox"
                        v-bind:checked="showSaleItem"
                        v-on:change="$emit('showSaleItemChanged')"
                    > セール対象</label>
                    <label><input type="checkbox"
                        v-bind:checked="showDelvFree"
                        v-on:change="$emit('showDelvFreeChanged')"
                    > 送料無料</label>
                </div>
                <!-- 並び替え条件 -->
                <div class="sort">
                    <label for="sort">並び替え</label>
                    <select id="sort" class="sorting"
                        v-bind:value="sortOrder"
                        v-on:change="$emit('sortOrderChanged', parseInt($event.target.value))"
                    >
                        <option value="1">標準</option>
                        <option value="2">価格が安い順</option>
                    </select>
                </div>
            </div><!-- /.condition -->
        </div><!-- /.search -->
    </header>
</template>

<script>
export default {
    name: 'ProdcutHeader',
    props: ['count', 'showSaleItem', 'showDelvFree', 'sortOrder'],
}
</script>

<style scoped>
/* ページのタイトルに対するpagetitleクラス */
.pagetitle {
    font-weight: normal;
    border-bottom: 2px solid;   /* 下線を引く */
}
/* 検索条件指定をまとめるsearchクラス */
.search {
    display: flex;  /* フレックスボックスにして小アイテムを横並びにする */
    justify-content: space-between; /* 子アイテムを等間隔で配置 */
}
.search .target {   /* searchクラス内のtargetクラス */
    display: inline-block;  /* 横並びでブロック表示 */
}
.search .target label { /* searchクラス内のtargetクラスのラベル */
    margin-right: 15px; /* 右外枠にスペース */
}
.search .sort {     /* searchクラス内のsortクラス */
    display: inline-block;  /* 横並びでブロック表示 */
}
</style>