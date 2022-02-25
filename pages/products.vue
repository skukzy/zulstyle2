<template>
  <div class="container">
    <Navigasi />
    <div class="row">
      <div class="col-md-12">
        <h1>Products</h1>
        <h1>{{ nama }}</h1>

        <div class="row">
          <div class="col-md-12">
            <!-- <h5 v-if="loading" class="text-center text-muted"><em>sedang memuat...</em></h5> -->
            <div class="text-center">
              <img v-if="loading" src="../static/assets/loading5.gif" width="400px">
            </div>
          </div>
          <div class="col-md-4" v-for="item in items" :key="item.id">
            <div class="card mb-5">
              <div class="card-header">
                <img :src="item.foto" class="img">
              </div>
              <div class="card-body">
                <h4>{{ item.nama }}</h4>
                <h4>Rp{{ item.harga }}</h4>
                <a :href="item.link_eksternal" class="btn btn-success btn-block">Pesan di WA</a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </div>
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
        .order('created_at', { ascending: false })

      if(data) {
        this.items = data
        this.loading = false
      }
      if(error) console.log(error)
    },
  }
}
</script>

<style scoped>
.card-header {
  padding: 0;
}
.card-header .img {
  width: 100%;
  border-radius: 5px;
}
.card {
  box-shadow: 5px 5px 0 #ddd;
  transition: all .3s ease;
}
.card:hover {
  transform: translateY(-10px);
}
</style>