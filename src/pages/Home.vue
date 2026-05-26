<script setup>
    import { Icon } from '@iconify/vue'
    import { computed, onMounted, ref } from 'vue'
    
    const date = ref("")
    const tanggalBuat = ref("")
    const title = ref("")
    const isShow = ref(false)
    
    const listHari = ref([])
    
    const newDate = () => {
        const newDate = new Date().toLocaleDateString('id-ID', {
            day: 'numeric',
            month: 'long',
            year: 'numeric'
        })
    
        date.value = newDate
    }
    
    const hitungHari = (tanggal) => {
        const today = new Date()
        const start = new Date(tanggal)
    
        today.setHours(0, 0, 0, 0)
        start.setHours(0, 0, 0, 0)
    
        const diffTime = today - start
        const diffDays = Math.floor(diffTime / (1000 * 60 * 60 * 24))
    
        return diffDays
    }
    
    const tambahHari = () => {
        if (!tanggalBuat.value || !title.value) return
    
        const data = {
            id: Date.now(),
            title: title.value,
            tanggal: tanggalBuat.value
        }
    
        listHari.value.push(data)
    
        localStorage.setItem("listHari", JSON.stringify(listHari.value))
    
        title.value = ""
        tanggalBuat.value = ""
        isShow.value = false
    }
    
    const hapusHari = (id) => {
        listHari.value = listHari.value.filter((item) => item.id !== id)
    
        localStorage.setItem("listHari", JSON.stringify(listHari.value))
    }
    
    onMounted(() => {
        newDate()
    
        const storage = localStorage.getItem("listHari")
    
        if (storage) {
            listHari.value = JSON.parse(storage)
        }
    })
</script>

<template>
    <!-- Modal -->
    <div v-if="isShow" class="min-h-screen w-full flex justify-center items-center absolute left-0 top-0 z-50">

        <div class="bg-black opacity-50 min-h-screen w-full absolute" @click="isShow = false"></div>

        <div class="absolute bg-white p-5 w-2/3 rounded-lg">
            <h3 class="font-bold text-xl mb-5">Tambah Hitungan</h3>

            <div class="flex flex-col gap-3">
                <input v-model="title" type="text" placeholder="Contoh: Mulai Tobat"
                    class="border p-2 rounded-lg w-full outline-none">

                <input v-model="tanggalBuat" type="date"
                    class="border p-2 rounded-lg w-full outline-none">

                <button @click="tambahHari"
                    class="bg-[#0F1B4C] text-white rounded-lg p-3 font-semibold">
                    Simpan
                </button>
            </div>
        </div>
    </div>

    <div class="bg-[#F5F6FB] min-h-screen p-5">

        <!-- Title -->
        <div class="flex justify-between items-center">
            <div>
                <h3 class="font-bold text-3xl text-[#0F1B4C]">
                    Hitung Hari
                </h3>

                <h5 class="w-3/4 text-[#6F7285]">
                    Hitung berapa hari sejak tanggal yang kamu pilih
                </h5>
            </div>

            <div>
                <div class="bg-white rounded-2xl p-3">
                    <Icon width="25" icon="picon:revert" />
                </div>
            </div>
        </div>

        <!-- Card -->
        <div class="mt-10 bg-linear-to-r from-[#7B6DFF] to-[#B39DFF] rounded-lg shadow-lg">

            <div class="p-5">
                <div class="flex items-center gap-3">

                    <div class="bg-white rounded-2xl p-3">
                        <Icon color="#0F1B4C" width="25" icon="akar-icons:schedule" />
                    </div>

                    <h4 class="text-white">
                        Hari ini
                    </h4>
                </div>
            </div>

            <div
                class="flex justify-between rounded-lg border-[#E9EAF3] text-sm bg-white pb-2 pt-2 pl-6 pr-6 items-center">

                <h3 class="text-gray-600">
                    Tanggal Hari Ini
                </h3>

                <h3 class="rounded-lg p-3 bg-[#F5F6FB] text-[#0F1B4C] font-semibold">
                    {{ date }}
                </h3>
            </div>
        </div>

        <!-- Add -->
        <div class="flex justify-between mt-5">
            <h3 class="font-semibold">
                Daftar Hitung Hari
            </h3>

            <button @click="isShow = true"
                class="text-[#0F1B4C] font-semibold shadow rounded-full px-5 py-1 bg-white">
                + Tambah
            </button>
        </div>

        <!-- Empty -->
        <div v-if="listHari.length === 0"
            class="bg-white rounded-lg shadow-md mt-5 p-10 flex flex-col items-center">

            <Icon icon="solar:calendar-outline" width="50" class="text-gray-400" />

            <h3 class="font-semibold mt-3">
                Belum ada data
            </h3>

            <p class="text-gray-500 text-sm">
                Tambahkan hitungan hari baru
            </p>
        </div>

        <!-- Card Total -->
        <div v-for="item in listHari" :key="item.id"
            class="bg-white rounded-lg shadow-md mt-5">

            <div class="p-3 flex justify-between">

                <div class="flex gap-3 items-center">

                    <div class="bg-[#F5F6FB] p-3 flex items-center rounded-lg w-15 h-15">
                        <Icon icon="material-symbols:schedule" width="30" height="30" />
                    </div>

                    <div>
                        <h4 class="font-semibold">
                            {{ item.title }}
                        </h4>

                        <h4 class="text-sm font-semibold text-gray-600">
                            {{ item.tanggal }}
                        </h4>

                        <h4 class="text-sm text-[#59C36A] font-semibold">
                            Dihitung Sejak
                        </h4>
                    </div>
                </div>

                <div class="flex items-center gap-2">

                    <div class="flex flex-col items-end">
                        <h3 class="font-bold text-3xl">
                            {{ hitungHari(item.tanggal) }}
                        </h3>

                        <h3>
                            hari
                        </h3>
                    </div>

                    <button @click="hapusHari(item.id)">
                        <Icon icon="mdi:delete-outline" width="25" class="text-red-500" />
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>