<template>
<section class="py-20">
  <div class="container">
    <!--- 商品卡片 --->
    <div class="row mt-9">
      <div class="col-md-3 mb-4" v-for="item in products" :key="item.id">
        <div class="card border-0 shadow-sm">
          <div style="height: 200px; background-size: cover; background-position: center;"
          :style="{backgroundImage: `url(${item.imageUrl})`}">
          </div>
          <div class="card-body" style="height: 136px">
            <div class="d-flex">
              <h5 class="card-title">{{ item.title }}</h5>
              <!-- <span class="badge bg-secondary float-right ml-2">{{ item.category }}</span> -->
            </div>
            <p class="card-text">{{ item.content }}</p>
            <div class="d-flex justify-content-between align-items-baseline">
              <div class="h5" v-if="!item.price">{{ item.origin_price }} 元</div>
              <del class="h6" v-if="item.price">原價 {{ item.origin_price }} 元</del>
              <div class="h5 text-danger" v-if="item.price">特價 {{ item.price }} 元</div>
            </div>
          </div>
          <div class="card-footer d-flex">
            <button type="button" class="btn btn-outline-secondary btn-sm">
              查看更多
            </button>
            <button type="button" class="btn btn-outline-danger btn-sm ms-auto">
              加到購物車
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>
</template>
<script>
export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    getProducts () {
      const vm = this
      const api = `${process.env.VUE_APP_APIPATH}/api/${process.env.VUE_APP_CUSTOMPATH}/admin/products/all`
      vm.$http.get(api).then((res) => {
        console.log('產品 All 列表', res.data)
        if (res.data.success) {
          vm.products = res.data.products
        } else {
          vm.$swal({ title: res.data.message, icon: 'error' })
        }
      })
    }
  },
  created () {
    this.getProducts()
  }
}
</script>
