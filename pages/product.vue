<template>
<main>
<navigasi/>
  <div class="container">
    <div class="row">
      <div class="col-md-10">
        <h3>Products</h3>

        <div class="row">
          <div class="col-md-12">
            <div v-if="loading" class="text-center">
              <img src="~/static/assets/loading.gif" alt="">
            </div>
          </div>
          <div class="col-md-3" v-for="item in items" :key="item.id">
            <div class="card mb-2">
              <div class="card-header">
                <img :src="item.foto" alt="" width="90%">
              </div>
              <div class="card-body">
                <h4>{{ item.nama }}</h4>
                <h4>Rp{{ item.harga }}</h4>
                <a :href="item.link_eksternal" class="btn btn-success btn-block">Beli di whatsapp</a>
              </div>
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
      items: '',
      loading: true,
    }
  },
  mounted() {
    this.ambilData()
  },
  methods: {
    async ambilData() {
      const { data, error } = await this.$supabase
        .from('tb_produk')
        .select()

      if(data) 
      this.items = data
      this.loading = false
      if(error) console.log(error)
    }
  }
}
</script>