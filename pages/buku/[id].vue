<template>
  <div class="container-fluid">
    <div class="row mt-4 d-flex justify-content-evenly">
      <div class="col-lg-4">
        <div class="card">
          <div class="card-body">
            <img src="~/assets/img/cover1.jpg" width="220px" height="340px" class="cover" alt="cover1">
          </div>
        </div>
      </div>
      <div class="col-4">
        <h5>Penulis: {{ Buku.penulis }}</h5>
        <h5>Penerbit: {{ Buku.penerbit }}</h5>
        <h5>Tahun terbit: {{ Buku.tahun_terbit }}</h5>
      </div>
    </div>
    <div class="row mt-5">
      <h2>Sinopsis</h2>
      <p class="mt-3"> Kisah ini menceritakan tentang Aily yang tuna netra dan Canva yang tidak pernah bahagia. Tentang Canva Narendra, salah satu anggota Diamond Gang yang memiliki sebuah luka dalam. Cita-citanya hanya satu, bertemu dengan kedua orang tuanya. Untuk itu, ia belajar dengan giat demi mencapai nilai yang tinggi dan mewujudkan cita-citanya, ditemani oleh anggota Diamond Gang dan juga seseorang yang ia cintai, Aily. Namun, kehadiran Zayyan Abrisam, musuh di masa lalu Canva yang memang cerdas dan selalu mendapatkan peringkat satu membuat hari-hari Canva semakin kacau. Rasa ambisi untuk menang dan mendapatkan juara satu menyebabkan Canva melupakan kesehatannya. Apakah Canva mampu untuk mewujudkan mimpinya? Atau, kesehatan lebih dulu merenggut apa yang ia citakan?</p>
    </div>
    <nuxt-link to="/buku">
      <button type="button" class="btn btn-dark mt-5">Kembali</button>
    </nuxt-link>
  </div>
</template>

<style scoped>
.card {
  width: 255px;
  height: 370px;
  box-shadow: 1px 1px 10px #424242;
}
</style>

<script setup>
const supabase = useSupabaseClient()

const route = useRoute()
const buku = ref([])

const getBookById = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  .eq('id', route.params.id)
  if(data) buku.value = data[0]
}

onMounted(() => {
  getBookById()
})
</script>