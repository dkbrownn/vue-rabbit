<script setup>
import ProductsItem from '../Home/components/ProductsItem.vue'
import { useToSubList } from './composables/useToSubList'
import { useGetSub } from './composables/useGetSub'
const { categoryList } = useToSubList()

/* const getCategoryList = async () => {
  const res = await getCategorySub(route.params.id)
  categoryList.value = res.data.result
}
onMounted(() => {
  getCategoryList()
}) */
const { productList, tabChange, reqData, load, disabled } = useGetSub()
/* const productList = ref([])
const reqData = ref({
  categoryId: route.params.id,
  page: 1,
  pageSize: 20,
  sortFiled: 'publishTime' 
})
const tabChange = () => {
  getProductList()
}
const getProductList = async () => {
  const res = await getSubCategory(reqData.value)
  productList.value = res.data.result.items
}
onMounted(()=>{
  getProductList()
}) */

</script>

<template>
  <div class="container ">
    <!-- 面包屑 -->
    <div class="bread-container">
      <el-breadcrumb separator=">">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item :to="`/category/${categoryList.parentId}`">{{categoryList.parentName}}
        </el-breadcrumb-item>
        <el-breadcrumb-item>{{categoryList.name}}</el-breadcrumb-item>
      </el-breadcrumb>
    </div>
    <div class="sub-container">
      <el-tabs v-model="reqData.sortFiled" @tab-change="tabChange">
        <el-tab-pane label="最新商品" name="publishTime" ></el-tab-pane>
        <el-tab-pane label="最高人气" name="orderNum"></el-tab-pane>
        <el-tab-pane label="评论最多" name="evaluateNum"></el-tab-pane>
      </el-tabs>
      <div class="body" v-infinite-scroll="load" :infinite-scroll-disabled="disabled">
         <!-- 商品列表-->
          <ProductsItem v-for="item in productList" :key="item.id" :good="item"/>
      </div>
    </div>
  </div>

</template>



<style lang="scss" scoped>
.bread-container {
  padding: 25px 0;
  color: #666;
}

.sub-container {
  padding: 20px 10px;
  background-color: #fff;

  .body {
    display: flex;
    flex-wrap: wrap;
    padding: 0 10px;
  }

  .goods-item {
    display: block;
    width: 220px;
    margin-right: 20px;
    padding: 20px 30px;
    text-align: center;

    img {
      width: 160px;
      height: 160px;
    }

    p {
      padding-top: 10px;
    }

    .name {
      font-size: 16px;
    }

    .desc {
      color: #999;
      height: 29px;
    }

    .price {
      color: $priceColor;
      font-size: 20px;
    }
  }

  .pagination-container {
    margin-top: 20px;
    display: flex;
    justify-content: center;
  }
}
::v-deep .el-tabs__item:hover{
    color: $xtxColor;
}
::v-deep .el-tabs__item.is-active{
  color: $xtxColor;
}
::v-deep .el-tabs__active-bar {
  background-color: $xtxColor;
}
</style>