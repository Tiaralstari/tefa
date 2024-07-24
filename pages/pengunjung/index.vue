<template>
    <html lang="en">
    <head>
        <meta charset="UT-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>menu</title>
    </head>
    <body>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">RIWAYAT KUNJUNGAN</h2>
                <nuxt-link to="../"><button type="submit" class="btn btn-lg rounded-5 px-5 bg-primary text-white" style="float: right; margin-bottom: 15px;">KEMBALI</button></nuxt-link>
                <div class="my-3">
                    <form @submit.prevent="getpengunjung">
                        <input v-model="keyword" type="search" class="form-control rounded-5"
                            placeholder="cari siapa?">
                    </form>
                </div>
                <div class="my-3 text-muted">menampilkan {{ visitors.length }} dari {{ jumlah }}</div>
                <table class="table table-border">
                    <thead>
                        <tr>
                            <td>#</td>
                            <td>NAMA</td>
                            <td>KEANGGOTAAN</td>
                            <td>WAKTU</td>
                            <td>KEPERLUAN</td>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(visitor, i) in visitors" :key="i">
                            <td>{{ i+1 }}</td>
                            <td>{{ visitor.nama }}</td>
                            <td>{{ visitor.keanggotaan.nama }}</td>
                            <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
                            <td>{{ visitor.keperluan.nama }}</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
    </body>
    </html>
</template>

<script setup>
useHead({title:'aplikasi perpus digital',
    meta:[{name:'description', content:'selamat mengunjung'}]
})
const supabase = useSupabaseClient()
const keyword = ref('')
const visitors = ref ([])
const jumlah = ref ([])

const getpengunjung = async () => {
    const {data,error} = await supabase.from('pengunjung').select(`*, keanggotaan(*), keperluan(*)`)
        .ilike('nama', `%${keyword.value}%`)
        .order(`id`, {ascending:false})
    if(data) visitors.value = data
}
const totalpengunjung = async () => {
    const { data, count } = await supabase.from('pengunjung')
    .select("*", {count: 'exact'})
    if (data) jumlah.value = count
}
onMounted(() =>{
    getpengunjung()
    totalpengunjung()
})
</script>