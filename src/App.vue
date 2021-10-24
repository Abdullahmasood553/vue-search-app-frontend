<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 m-auto mt-4">
        <div class="form-group">
          <input type="text" v-model="keyword" class="form-control form-control-lg" placeholder="Search Product">
          <div v-if="products?.length > 0">
            <div v-for="product in products" :key="product.id">
              <div class="card card-body mb-1">
                <h6 class="text-white" v-text="product.title"></h6>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'App',
    components: {},
    data() {
      return {
        keyword: '',
        products: Array,
      }
    },
    watch: {
      keyword: function () {
        this.getResults()
      }
    },
    methods: {
      getResults: function () {
        axios.get('http://localhost:8000/api/products/backend?search=' + this.keyword)
          .then(res => this.products = res.data)
          .catch(error => {
            console.log(error);
          });
      }
    },
    mounted() {
      console.log('Search Component');
    }
  }
</script>