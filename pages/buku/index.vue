<template>
  <div class="content">
    <div class="container-fluid">
      <div class="row">
        <div class="col-lg-12">
          <nuxt-link to="/pengunjung">
            <button type="button" class="btn btn-outline-dark mt-4 btn-lg">KEMBALI</button>
          </nuxt-link>
            <h2 class="text-center my-4 fw-bold">RAK BUKU</h2>
            <form @submit.prevent="getBooks" class="col mb-3">
              <div class="input-group flex-nowrap rounded">
                <input v-model="keyword" type="search" class="form-control from-control-lg rounded-5" placeholder="Cari Judul..." aria-label="Search" @input="getbooks" />
              </div>
            </form>
            <div class="my-3">Menampilkan {{ books.length }} buku dari {{ jmlbuku }}</div>
          </div>
        </div>
          <div class="row shadow-lg">
              <div v-for="(book,i) in books" :key="i" class="col">
                  <div class="card mb-3 col-lg-2 col-2">
                    <nuxt-link :to="`/buku/${book.id}`">
                      <div class="card-body">
                        <img :src="book.cover" class="cover" alt="cover">
                      </div>
                    </nuxt-link>
                  </div>
              </div>
          </div>
    </div>
  </div>
</template>

<script setup>
const supabase= useSupabaseClient()

const keyword = ref('')
const books = ref([])
const jmlbuku = ref(0)

const getbooks = async () => {
  const { data ,error } = await supabase
  .from('buku')
  .select(`*, kategori(*)`)
  .ilike("judul", `%${keyword.value}%`)
  .order('id')
  if(data) books.value = data
}
const getJmlBuku = async () => {
  const{ data, count } = await supabase
    .from("buku") 
    .select('*', { count: "exact" })
    if(data) jmlbuku.value = count
}

onMounted(() =>{
  getbooks()
  getJmlBuku()

})
</script>
