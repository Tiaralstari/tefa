<template>
    <div class="container-fluid">
        <div class="row">
            <div class="col-lg-12">
                <h2 class="text-center my-4">BUKU</h2>
                <nuxt-link to="../"><button type="submit" class="btn btn-lg rounded-5 px-5 bg-primary text-white"
                        style="float: right; margin-bottom: 15px;">KEMBALI</button></nuxt-link>
                <div class="my-3">
                    <form @submit.prevent="getBooks">
                        <input v-model="keyword" type="search" class="form-control rounded-5"
                            placeholder="Mau baca apa hari ini?">
                    </form>
                </div>
                <div class="my-3 text-muted">menampilkan {{ books.length }} dari {{ books.length }} buku </div>
                <div class="row">
                    <div v-for="(book, i) in books" :key="i" class="col-lg-2">
                        <div class="card mb-4">
                            <NuxtLink :to="`/buku/${book.id}`">
                            <img :src="book.cover" class="cover" alt="cover">
                            </NuxtLink>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const keyword = ref('')
const books = ref([])

const getBooks = async () => {
    const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
        .ilike('judul', `%${keyword.value}%`)
    if (data) books.value = data
}
const totalBuku = async () => {
    const { data, count } = await supabase.from ('buku')
    .select("*", {count: 'exact'})
    if (data) jumlah.value = count
}

onMounted(() => {
    getBooks()
})
</script>

<style scoped>
.card-body {
    width: 100%;
    height: 20em;
    padding: 0;
}

.cover {
    width: 100%;
    height: 20em;
    object-fit: cover;
    object-position: 0 30;
}
</style>