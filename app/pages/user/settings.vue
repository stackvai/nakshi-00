<!-- pages/user/settings.vue -->
<script setup lang="ts">
import { ref } from 'vue'

definePageMeta({ layout: 'user' })
useHead({ title: 'প্রোফাইল সেটিংস — নকশী কাঁথা স্টুডিও' })

const profile = ref({ name: 'আবদুল বাসেত', email: 'bappy@example.com', phone: '01700000000' })
const successAlert = ref(false)

const handleUpdate = () => {
  successAlert.value = true
  setTimeout(() => { successAlert.value = false }, 4000)
}
</script>

<template>
  <div class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-8 space-y-6 shadow-sm">
    <div class="border-b border-slate-100 pb-4">
      <h1 class="text-xl sm:text-2xl font-bold font-serif text-slate-900">প্রোফাইল সেটিংস</h1>
      <p class="text-xs text-slate-500 mt-0.5">আপনার ব্যক্তিগত তথ্য ও পাসওয়ার্ড আপডেট করুন</p>
    </div>

    <div v-if="successAlert" class="p-3 bg-emerald-50 border border-emerald-200 text-emerald-800 text-xs rounded-xl">
      ✅ প্রোফাইল সফলভাবে আপডেট করা হয়েছে!
    </div>

    <form @submit.prevent="handleUpdate" class="space-y-4 max-w-xl">
      <div class="space-y-1">
        <label class="text-xs font-bold text-slate-700">পূর্ণ নাম</label>
        <input v-model="profile.name" type="text" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900 bg-slate-50" />
      </div>
      <div class="space-y-1">
        <label class="text-xs font-bold text-slate-700">ইমেইল ঠিকানা</label>
        <input v-model="profile.email" type="email" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900 bg-slate-50" />
      </div>
      <div class="space-y-1">
        <label class="text-xs font-bold text-slate-700">মোবাইল নম্বর</label>
        <input v-model="profile.phone" type="tel" class="w-full px-4 py-3 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900 bg-slate-50" />
      </div>
      <button type="submit" class="bg-rose-900 hover:bg-rose-950 text-white font-bold text-xs px-6 py-3 rounded-xl transition-colors">
        পরিবর্তন সেভ করুন 💾
      </button>
    </form>
  </div>
</template>