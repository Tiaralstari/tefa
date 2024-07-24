<template>
    <div class="container-fluid">
        <div class="row my-5 justify-content-around">
            <div class="col-lg-5">
                <nuxt-link to="/pengunjung/tambah">
                    <div class="card bg-pengunjung rounded-5">
                        <div class="card-body">
                            <h2>pengunjung</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>
            <div class="col-lg-5">
                <nuxt-link to="/buku">
                    <div class="card bg-buku rounded-5">
                        <div class="card-body">
                            <h2 style="font-family: ;">cari buku</h2>
                        </div>
                    </div>
                </nuxt-link>
            </div>

        <div class="mt-5" style="margin-left: 200px">
            <h2 class=" ">STATISTIK</h2>
        </div>
    </div>
    </div>

    <div class="container-fluid">
        <div class="row my-5 justify-content-around">
            <div class="col-lg-5">
                    <div class="card bg-warning rounded-5 mt-5">
                        <div class="card-body">
                            <h2 class="font"> {{ jumlahpengunjung }} Pengunjung</h2>
                        </div>
                    </div>
            </div>

            <div class="col-lg-5">
                    <div class="card bg-primary rounded-5 mt-5">
                        <div class="card-body">
                            <h1 class="font"> {{jumlahbuku}} Buku</h1>   
                        </div>
                    </div>
            </div>
        </div>
            <Chart />
    </div>
</template>

<script setup>
const supabase = useSupabaseClient()
const jumlahpengunjung = ref (0)
const jumlahbuku = ref (0)

async function ambiljumlahpengunjung() {
    const { data,error, count} = await supabase
    .from("pengunjung")
    .select("*", {count: 'exact'});
    if (count) jumlahpengunjung.value = count;
}
async function ambiljumlahbuku() {
    const { data,error, count} = await supabase
    .from("buku")
    .select("*", {count: 'exact'});
    if (count) jumlahbuku.value = count;
}


onMounted(() => {
    ambiljumlahpengunjung();
    ambiljumlahbuku();
})
</script>

<style scoped>
.card {
    height: 250px;
    box-shadow: 1px 1px 10px  #424242;
}
.card.bg-pengunjung {
    background-image: url('../assets/img/bg-home-kunjungan.jpeg') ;
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
    opacity: 70%;
}
.card.bg-buku {
    background: url('../assets/img/bg-home-cari-buku.jpg') no-repeat center center;
    background-size: cover;
    opacity: 70%;
}

h4{
    color: black;
    font-size: 40px;
    text-align: margin-left;
    margin: 40px;
    opacity: 70%;
}

h2{
    color: black;
    font-size: 40px;
    text-align:margin-left ;
    margin: my-40px;
}
 
h3{
    color: black;
    font-size: 60px;
    text-align: center;
    margin: 60px;
}
</style>