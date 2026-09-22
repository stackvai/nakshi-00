<!-- pages/user/addresses.vue -->
<script setup lang="ts">
import { ref } from 'vue'

definePageMeta({ layout: 'user' })
useHead({ title: 'ডেলিভারি ঠিকানা — নকশী কাঁথা স্টুডিও' })

const addresses = ref([
  { id: 1, name: 'আবদুল বাসেত', phone: '01700000000', address: 'বাসা ১২, রোড ৩, ধানমন্ডি', city: 'ঢাকা', isDefault: true }
])

const showAddModal = ref(false)
const newAddress = ref({ name: '', phone: '', address: '', city: 'ঢাকা' })

const handleAdd = () => {
  addresses.value.push({ id: Date.now(), ...newAddress.value, isDefault: false })
  newAddress.value = { name: '', phone: '', address: '', city: 'ঢাকা' }
  showAddModal.value = false
}
</script>

<template>
  <div class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-8 space-y-6 shadow-sm">
    <div class="flex justify-between items-center border-b border-slate-100 pb-4">
      <div>
        <h1 class="text-xl sm:text-2xl font-bold font-serif text-slate-900">ডেলিভারি ঠিকানা</h1>
        <p class="text-xs text-slate-500 mt-0.5">আপনার শিপিং অ্যাড্রেস ম্যানেজ করুন</p>
      </div>
      <button @click="showAddModal = true" class="bg-rose-900 hover:bg-rose-950 text-white font-bold text-xs px-4 py-2.5 rounded-xl transition-colors">
        + নতুন ঠিকানা যোগ করুন
      </button>
    </div>

    <!-- Address Cards -->
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
      <div v-for="addr in addresses" :key="addr.id" class="p-5 rounded-2xl border border-slate-200/80 bg-slate-50/50 space-y-2 relative">
        <span v-if="addr.isDefault" class="absolute top-4 right-4 bg-amber-100 text-amber-900 text-[10px] font-bold px-2.5 py-0.5 rounded-full">ডিফল্ট</span>
        <h3 class="font-bold text-sm text-slate-900 font-serif">{{ addr.name }}</h3>
        <p class="text-xs text-slate-600">ফোন: {{ addr.phone }}</p>
        <p class="text-xs text-slate-600">{{ addr.address }}, {{ addr.city }}</p>
      </div>
    </div>

    <!-- Add Modal -->
    <div v-if="showAddModal" class="fixed inset-0 z-50 bg-slate-950/60 backdrop-blur-sm flex items-center justify-center p-4">
      <div class="bg-white rounded-3xl max-w-md w-full p-6 sm:p-8 space-y-4 relative shadow-2xl">
        <button @click="showAddModal = false" class="absolute top-4 right-4 text-slate-400 font-bold">✕</button>
        <h3 class="font-serif text-lg font-bold text-slate-900">নতুন ঠিকানা যোগ করুন</h3>
        <form @submit.prevent="handleAdd" class="space-y-4">
          <input v-model="newAddress.name" type="text" required placeholder="প্রাপকের নাম" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900" />
          <input v-model="newAddress.phone" type="tel" required placeholder="মোবাইল নম্বর" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900" />
          <input v-model="newAddress.address" type="text" required placeholder="বাসা/রোড/এলাকা" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900" />
          <input v-model="newAddress.city" type="text" required placeholder="শহর/জেলা" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900" />
          <button type="submit" class="w-full bg-rose-900 text-white font-bold py-3 rounded-xl text-xs">সেভ করুন</button>
        </form>
      </div>
    </div>
  </div>
</template>