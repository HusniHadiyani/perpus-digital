<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
        <div class="my-3">
          <form @submit.prevent="getPengunjung">
            <input v-model="keyword" type="serch" class="form-conrol form-control-lg rounded-5" placeholder="Mencari..." />
          </form>
        </div>
        <div class="my-3">Menampilkan {{ visitors.length }} Dari {{ Semua }}</div>
        <table class="table">
          <thead>
            <tr>
              <td>No</td>
              <td>Tanggal/Waktu</td>
              <td>Nama</td>
              <td>Keanggotaan</td>
              <td>Tingkat</td>
              <td>Jurusan</td>
              <td>Kelas</td>
              <td>Keperluan</td>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(visitor, i) in visitors" :key="i">
              <td>{{ i + 1 }}.</td>
              <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
              <td>{{ visitor.nama }}</td>
              <td>{{ visitor.keanggotaan.nama }}</td>
              <td>{{ visitor.tingkat }}</td>
              <td>{{ visitor.jurusan }}</td>
              <td>{{ visitor.kelas }}</td>
              <td>{{ visitor.keperluan.nama }}</td>
            </tr>
          </tbody>
        </table>      
       <NuxtLink to="/">
          <button type="submit" class="btn btn-dark btn-lg rounded-5 px-5">Menu</button>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient();

const Semua = ref(0);

const keyword = ref("");

const visitors = ref([]);

const getPengunjung = async () => {

  const { data, error } = await supabase

    .from("Pengunjung")

    .select(`*, keanggotaan(nama), keperluan(nama)`)

    .order("id", { ascending: false })

    .ilike("nama", `%${keyword.value}%`);

  if (data) visitors.value = data;

};


const getJumlah = async () => {

  const { data, error } = await supabase

    .from("jumlahpengunjung")

    .select()

    .single()

  if (data) Semua.value = data.jumlahpengunjung

};

onMounted(() => {

  getPengunjung();

  getJumlah();

});

</script>
