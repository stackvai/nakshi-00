<!-- pages/user/wishlist.vue -->
<script setup lang="ts">
import { ref } from 'vue'

definePageMeta({
  layout: 'user'
})

useHead({
  title: 'উইশলিস্ট বা পছন্দসমূহ — নকশী কাঁথা স্টুডিও'
})

// Mock wishlist items
const wishlistItems = ref([
  { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', price: 4500, originalPrice: 5200, image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 2, title: 'ঐতিহ্যবাহী শাপলা কদম নকশী কাঁথা', price: 3800, originalPrice: 4200, image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' }
])

const removeItem = (id: number) => {
  wishlistItems.value = wishlistItems.value.filter(item => item.id !== id)
}
</script>

<template>
  <div class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-8 space-y-6 shadow-sm">
    <div class="flex justify-between items-center border-b border-slate-100 pb-4">
      <div>
        <h1 class="text-xl sm:text-2xl font-bold font-serif text-slate-900">আমার উইশলিস্ট</h1>
        <p class="text-xs text-slate-500 mt-0.5">আপনার পছন্দ করা ফেভারিট পণ্যসমূহ</p>
      </div>
      <span class="bg-rose-50 text-rose-900 font-bold text-xs px-3 py-1 rounded-full border border-rose-100">
        {{ wishlistItems.length }} টি পণ্য
      </span>
    </div>

    <!-- Empty State -->
    <div v-if="wishlistItems.length === 0" class="text-center py-16 space-y-3">
      <span class="text-4xl">❤️</span>
      <h3 class="font-bold text-base font-serif text-slate-800">আপনার উইশলিস্ট খালি</h3>
      <p class="text-xs text-slate-500">শপ থেকে আপনার পছন্দের পণ্যে হার্ট আইকনে ক্লিক করে এখানে সেভ করুন।</p>
      <NuxtLink to="/shop" class="inline-block mt-2 bg-rose-900 text-white text-xs font-bold px-6 py-3 rounded-xl">
        শপ ভিজিট করুন 🛍️
      </NuxtLink>
    </div>

    <!-- Wishlist Grid -->
    <div v-else class="grid grid-cols-1 sm:grid-cols-2 gap-6">
      <div v-for="item in wishlistItems" :key="item.id" class="border border-slate-200/80 rounded-2xl overflow-hidden bg-white shadow-sm flex flex-col justify-between group">
        <div>
          <div class="aspect-[4/3] overflow-hidden bg-slate-100 relative">
            <button @click="removeItem(item.id)" class="absolute top-3 right-3 z-10 w-8 h-8 rounded-full bg-white/90 text-rose-700 font-bold flex items-center justify-center shadow-md hover:bg-rose-900 hover:text-white transition-colors">
              ✕
            </button>
            <img :src="item.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" alt="Wishlist item" />
          </div>
          <div class="p-4 space-y-1">
            <h3 class="font-bold text-sm text-slate-800 font-serif line-clamp-1">{{ item.title }}</h3>
            <div class="flex items-center gap-2">
              <span class="text-base font-extrabold text-rose-950">৳ {{ item.price }}</span>
              <span class="text-xs text-slate-400 line-through">৳ {{ item.originalPrice }}</span>
            </div>
          </div>
        </div>
        <div class="p-4 pt-0">
          <button class="w-full bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold py-2.5 rounded-xl transition-colors shadow-sm">
            কার্টে যোগ করুন 🛒
          </button>
        </div>
      </div>
    </div>
  </div>
</template>