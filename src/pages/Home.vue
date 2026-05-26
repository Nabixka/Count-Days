<script setup>
import { Icon } from '@iconify/vue';
import { onMounted, ref } from 'vue';

const date = ref("")

const newDate = new Date().toLocaleDateString('id-ID', {
    day: 'numeric', 
    month: 'long',
    year: 'numeric'
}
)
date.value = newDate
</script>

<template>
    <div class="bg-[#F5F6FB] min-h-screen p-5">

        <!-- Title -->
        <div class="flex justify-between items-center">
            <div class="">
                <h3 class="font-bold text-3xl text-[#0F1B4C]">Hitung Hari</h3>
                <h5 class="w-3/4 text-[#6F7285]">Hitung berapa hari dan tanggal yang kamu pilih</h5>
            </div>
            <div>
                <div class="bg-white rounded-2xl p-3">
                    <Icon width="25"  icon="picon:revert"/>
                </div>
            </div>
        </div>

        <!-- Card -->
        <div class="mt-10 bg-linear-to-r from-[#7B6DFF] to-[#B39DFF] rounded-lg shadow shadow-lg">
            <div class="p-5">
                <div class="flex items-center gap-3">
                    <div class="bg-white rounded-2xl p-3">
                        <Icon color="#0F1B4C" width="25" icon="akar-icons:schedule"/>
                    </div>
                    <h4 class="text-white">Kamu sudah</h4>
                </div>
            </div>

            <div class="flex justify-between rounded-lg border-[#E9EAF3] text-sm bg-white pb-2 pt-2 pl-6 pr-6 items-center">
                <h3 class="text-gray-600">Tanggal Hari Ini</h3>
                <h3 class="rounded-lg p-3 bg-[#F5F6FB] text-[#0F1B4C] font-semibold">{{ date }}</h3>
            </div>
        </div>

        <!-- Add -->
        <div class="flex justify-between mt-5">
            <h3 class="font-semibold">Daftar Hitung Hari</h3>
            <button class="text-[#0F1B4C] font-semibold shadow rounded-full px-5 py-1 ">
                + Tambah
            </button>
        </div>

        <!-- Card Total -->
        <div class="bg-white rounded-lg shadow-md mt-5">
            <div class="p-3 flex justify-between">

                <div class="flex gap-3 items-center">
                    <div class="bg-[#F5F6FB] p-3 flex items-center rounded-lg w-15 h-15">
                        <Icon icon="material-symbols:schedule" width="30" height="30"/>
                    </div>
                    <div>
                        <h4 class="font-semibold">Mulai Tobat</h4>
                        <h4 class="text-sm font-semibold text-gray-600">26/05/2026</h4>
                        <h4 class="text-sm text-[#59C36A] font-semibold">Dihitung Sejak</h4>
                    </div>
                </div>

                <div class="flex items-center">
                    <div class="flex flex-col items-end">
                        <h3 class="font-bold text-3xl">80</h3>
                        <h3>hari</h3>
                    </div>
                    <Icon icon="iwwa:option" width="45" height="25"></Icon>
                </div>
            </div>
        </div>

    </div>
</template>