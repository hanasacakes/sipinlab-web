<script setup>
import { ref } from 'vue'
import BaseButton from '@/components/base/BaseButton.vue'
import BaseInput from '@/components/base/BaseInput.vue'
import StatusBadge from '@/components/base/StatusBadge.vue'
import StatCard from '@/components/base/StatCard.vue'

const varian = ['primary', 'secondary', 'danger', 'ghost']
const daftarStatus = [
  'baik',
  'rusak_ringan',
  'rusak_berat',
  'dipinjam',
  'dikembalikan',
  'terlambat',
  'admin',
  'petugas',
]

const nama = ref('')
const merek = ref('Olympus')
const kode = ref('OPT-001')
const catatan = ref('')
</script>

<template>
  <main class="halaman">
    <div class="page-header">
      <div>
        <h1>Design System</h1>
        <p>Pameran semua varian komponen dasar SIPINLAB.</p>
      </div>
    </div>

    <section class="card bagian">
      <h2 class="card-title">BaseButton</h2>
      <div class="baris">
        <BaseButton v-for="v in varian" :key="v" :variant="v">{{ v }}</BaseButton>
      </div>
      <div class="baris">
        <BaseButton v-for="v in varian" :key="v" :variant="v" size="sm">{{ v }} (sm)</BaseButton>
      </div>
      <div class="baris">
        <BaseButton loading>Memuat</BaseButton>
        <BaseButton disabled>Nonaktif</BaseButton>
      </div>
      <BaseButton block>Tombol penuh (block)</BaseButton>
    </section>

    <section class="card bagian">
      <h2 class="card-title">BaseInput</h2>
      <BaseInput v-model="nama" label="Normal" placeholder="Nama alat" />
      <BaseInput v-model="merek" label="Dengan hint" hint="Contoh: Olympus, Pyrex" />
      <BaseInput v-model="kode" label="Galat" error="Kode sudah digunakan." required />
      <BaseInput v-model="catatan" label="Textarea" type="textarea" placeholder="Catatan" />
    </section>

    <section class="card bagian">
      <h2 class="card-title">StatusBadge</h2>
      <div class="baris">
        <StatusBadge v-for="s in daftarStatus" :key="s" :value="s" />
      </div>
    </section>

    <section class="bagian">
      <h2 class="card-title">StatCard</h2>
      <div class="grid-stat">
        <StatCard label="Total alat" :value="15" icon="box" tone="primary" note="Semua kategori" />
        <StatCard label="Tersedia" :value="12" icon="check" tone="success" />
        <StatCard label="Stok menipis" :value="3" icon="alert" tone="warning" />
        <StatCard label="Terlambat" :value="1" icon="clipboard" tone="danger" />
      </div>
    </section>
  </main>
</template>

<style scoped>
.halaman {
  max-width: 960px;
  margin: var(--space-6) auto;
  padding: 0 var(--space-4);
}
.bagian {
  margin-bottom: var(--space-5);
}
.baris {
  display: flex;
  flex-wrap: wrap;
  gap: var(--space-3);
  align-items: center;
  margin-bottom: var(--space-4);
}
.grid-stat {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: var(--space-4);
}
</style>
