<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <input type="serch" class="form-conrol form-control-lg rounded-5" placeholder="Filter..." />
        </div>
        <div class="my-3 text-muted">menampilkan 1 dari 1</div>
        <table class="table">
          <thead>
            <tr>
              <td>NO</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>1.</td>
              <td>Husni Hadiyani</td>
              <td>Siswa</td>
              <td>26 Februari 2024, 14.5</td>
              <td>Membaca</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
    <nuxt-link to="/buku"></nuxt-link>
    <button type="button" class="btn btn-dark mt-5">Kembali</button>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref({})

const getPengunjung = async () => {
  const { data, error } =await supabase.from('pengunjung').select('*, keanggotaan(*), keperluan(*)')
}

onMounted(()=> {
  getPengunjung()
})

<tbody>
  <tr v-for="(visitor.i) in visitor" :key="i">
    <td> {{ i+1 }}.</td>
    <td>{{ visitor.nama }}</td>
    <td>{{ visitor.keanggotaan.nama }}</td>
    <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
    <td>{{ visitor.keperluan.nama }}</td>
  </tr> 
</tbody>


</script>