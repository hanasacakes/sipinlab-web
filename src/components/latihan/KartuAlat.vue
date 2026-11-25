<script setup>
import { computed } from 'vue'

const props = defineProps({
  kode: { type: String, required: true },
  nama: { type: String, required: true },
  tersedia: { type: Number, default: 0 },
  total: { type: Number, default: 0 },
  kondisi: {
    type: String,
    default: 'baik',
    validator: (nilai) => ['baik', 'rusak_ringan', 'rusak_berat'].includes(nilai),
  },
})

const emit = defineEmits(['pinjam', 'kembali'])

const labelKondisi = computed(
  () =>
    ({
      baik: 'Baik',
      rusak_ringan: 'Rusak ringan',
      rusak_berat: 'Rusak berat',
    })[props.kondisi],
)
</script>

<template>
  <article class="kartu" :class="{ habis: tersedia === 0 }">
    <div class="atas">
      <span class="kode">{{ kode }}</span>
      <span class="lencana" :class="kondisi">{{ labelKondisi }}</span>
    </div>
    <h3>{{ nama }}</h3>
    <p>
      Tersedia <strong>{{ tersedia }}</strong> dari {{ total }} unit
    </p>
    <p v-if="tersedia === 0" class="label-habis">Stok habis</p>

    <div class="aksi">
      <button :disabled="tersedia === 0" @click="emit('pinjam', kode)">Pinjam 1 unit</button>
      <button class="kembali" :disabled="tersedia >= total" @click="emit('kembali', kode)">
        Kembalikan 1 unit
      </button>
    </div>
  </article>
</template>

<style scoped>
.kartu {
  border: 1px solid #e2e8f0;
  border-radius: 12px;
  padding: 16px;
  background: #fff;
}
.kartu.habis {
  opacity: 0.6;
}
.atas {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.kode {
  font-size: 12px;
  color: #64748b;
}
.lencana {
  font-size: 12px;
  font-weight: 600;
  padding: 2px 8px;
  border-radius: 999px;
}
.lencana.baik {
  background: #dcfce7;
  color: #166534;
}
.lencana.rusak_ringan {
  background: #fef3c7;
  color: #92400e;
}
.lencana.rusak_berat {
  background: #fee2e2;
  color: #b91c1c;
}
h3 {
  margin: 4px 0 8px;
}
.label-habis {
  color: #b91c1c;
  font-weight: 600;
}
.aksi {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-top: 8px;
}
button {
  padding: 8px 12px;
  border: 0;
  border-radius: 8px;
  background: #0e7c66;
  color: #fff;
  cursor: pointer;
}
button.kembali {
  background: #fff;
  color: #0e7c66;
  border: 1px solid #0e7c66;
}
button:disabled {
  background: #94a3b8;
  color: #fff;
  border-color: #94a3b8;
  cursor: not-allowed;
}
</style>
