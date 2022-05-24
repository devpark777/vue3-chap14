<template>
  <main class="mt-3">
    <div class="container">
      <div class="row mb-2">
        <div class="col-12">
          <h5>상품종류</h5>
          <select class="form-select">
            <option selected></option>
            <option value="1">여자옷</option>
            <option value="2">남자옷</option>
            <option value="3">마우스/키보드</option>
          </select>
        </div>
      </div>
      <div class="row">
        <div class="col-xl-3 col-lg-4 col-md-6" :key="i" v-for="(product,i) in productList.content">
          <div class="card" style="width: 18rem;">
            <h5 class="card-title">{{product.itemNm}}</h5>
            <a @click="goToDetail(product.id);" style="cursor:pointer;">    
              <!-- <img src="http://localhost:8090/images/item/bb2a945d-3646-4a97-88ca-79865fb364e7.jpg"> -->
              <img :src="`http://localhost:8090${product.imgUrl}`" class="card-img-top" alt="상품 이미지">
            </a>

            <div class="card-body">
              <h5 class="card-title">{{product.itemDetail}}</h5>
            
              <div class="d-flex justify-content-between align-items-center">
                <div class="btn-group" role="group">
                  <button type="button" class="btn btn-sm btn-primary">장바구니 담기</button>
                  <button type="button" class="btn btn-sm btn-danger">주문하기</button>
                </div>
                <small class="text-dark">{{product.price}}원</small>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      productList: []
    };
  },
  created() {
    this.getProductList();
    console.log(this.productList)
  },
  methods: {
    async getProductList() {
      this.productList = await this.$api("/api/productList2",{});
      // this.productList = await this.$apiPost("/api/productList2",{param:{userId:"testId", password:"pwd"}});
      // this.productList = await this.$apiPost("/api/productList2",{});
      
      // this.productList = await this.$api("/api/user","get");
      
      console.log("상품리스트===>",this.productList);
      
    },    
    goToDetail(product_id) {
     this.$router.push({path:'/detail', query:{ product_id:product_id }}); 
    }
  }
}
</script>