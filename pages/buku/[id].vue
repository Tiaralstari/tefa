<template>
    <div class="container-fluid">
        <h2 class="text-start my-4">{{ buku.judul }}</h2>
        <div class="row">
            <div class="col-md-3">
                <span v-if="buku.cover"><img :src="buku.cover" :alt="buku.judul"/></span>
            </div>
            <div class="col-md-8">
                <div class="badge bg-primary p-2">{{ buku.kategori }}</div>
                <ul class="list-group list-group-flush">
                    <li class="list-group-item">Penulis : {{ buku.penulis }}</li>
                    <li class="list-group-item">Penerbit : {{ buku.penerbit }}</li>
                    <li class="list-group-item">Tahun terbit : {{ buku.tahun_terbit }}</li>
                    <li class="list-group-item">{{ buku.deskripsi }}</li>
                </ul>
            </div>
        </div class="" style="margin-left:10px">
        <nuxt-link to="../"><button type="submit" class="btn btn-lg rounded-5 px-5 bg-primary text-white"
                            style="float: right; margin-top: 30px;">PINJAM</button></nuxt-link>
        <nuxt-link to="../"><button type="submit" class="btn btn-lg rounded-5 px-5 bg-secondary text-white"
                            style="float: right; margin-right: 30px; margin-top: 30px;">KEMBALI</button></nuxt-link>
    </div>
</template>


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

<style scoped>
.cover {
    height: 430px;
    width: 340px;
}
.card.mb-8 {
    margin-top: 50px;
    height: 340px;
    width: 235px;
}
h2{
    margin-top: 50px;
    margin-bottom: 1px;
}
p {
    margin-left: 20px;
    margin-bottom: 7px;
}
</style>
