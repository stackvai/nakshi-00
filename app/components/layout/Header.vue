<!-- components/layout/Header.vue -->
<script setup lang="ts">
import { ref } from 'vue'

const searchQuery = ref('')
const isCartOpen = ref(false)
const isWishlistOpen = ref(false)
const isUserMenuOpen = ref(false)

// Mock reactive cart items
const cartItems = ref([
  { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা', price: 4500, qty: 1, image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=200' },
  { id: 3, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো', price: 1850, qty: 1, image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=200' }
])

// Mock reactive wishlist items
const wishlistItems = ref([
  { id: 2, title: 'ঐতিহ্যবাহী শাপলা কদম নকশী কাঁথা', price: 3800, image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=200' },
  { id: 4, title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট', price: 3200, image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=200' }
]
)

const cartSubtotal = computed(() => {
  return cartItems.value.reduce((acc, item) => acc + (item.price * item.qty), 0)
})

const handleSearch = () => {
  if (searchQuery.value.trim()) {
    navigateTo(`/shop?q=${encodeURIComponent(searchQuery.value)}`)
  }
}
</script>

<template>
  <header class="bg-white sticky top-0 z-40 shadow-sm border-b border-slate-100">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-3.5 flex items-center justify-between gap-4 md:gap-8">
      
      <!-- Brand Logo -->
      <NuxtLink to="/" class="flex items-center gap-3 group shrink-0" aria-label="নকশী কাঁথা হোম পেজ">
        <div class="w-10 h-10 sm:w-12 sm:h-12 rounded-full bg-gradient-to-tr from-rose-900 to-amber-700 flex items-center justify-center text-white font-bold text-xl shadow-md group-hover:scale-105 transition-transform">
          ন
        </div>
        <div class="flex flex-col">
          <span class="text-xl sm:text-2xl font-bold tracking-tight text-rose-950 font-serif">
            নকশী<span class="text-amber-700">কাঁথা</span>
          </span>
          <span class="text-[10px] sm:text-xs text-slate-500 font-medium tracking-widest -mt-1">
            হস্তশিল্প ও ঐতিহ্য
          </span>
        </div>
      </NuxtLink>

      <!-- Global Search Bar -->
      <form @submit.prevent="handleSearch" class="hidden md:flex flex-1 max-w-xl relative">
        <input
          v-model="searchQuery"
          type="search"
          placeholder="কাঁথা, বেডশীট, কুশন কভার খুঁজুন..."
          class="w-full pl-4 pr-12 py-2.5 rounded-full border border-slate-200 focus:outline-none focus:border-rose-800 focus:ring-1 focus:ring-rose-800 text-sm transition-all bg-slate-50 focus:bg-white"
        />
        <button
          type="submit"
          aria-label="Search"
          class="absolute right-1.5 top-1/2 -translate-y-1/2 bg-rose-900 text-white p-2 rounded-full hover:bg-rose-950 transition-colors"
        >
          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/>
          </svg>
        </button>
      </form>

      <!-- User Actions & Dropdowns -->
      <div class="flex items-center gap-3 sm:gap-4">
        
        <!-- 1. Wishlist Dropdown Container -->
        <div class="relative" @mouseenter="isWishlistOpen = true" @mouseleave="isWishlistOpen = false">
          <NuxtLink to="/user/wishlist" class="relative p-2 text-slate-700 hover:text-rose-900 transition-colors flex items-center justify-center" aria-label="উইশলিস্ট">
            <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.8" d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"/>
            </svg>
            <span v-if="wishlistItems.length" class="absolute top-0 right-0 bg-amber-600 text-white text-[10px] font-bold w-4 h-4 rounded-full flex items-center justify-center">
              {{ wishlistItems.length }}
            </span>
          </NuxtLink>

          <!-- Wishlist Animated Dropdown -->
          <div v-show="isWishlistOpen" class="absolute right-0 top-full w-80 bg-white rounded-2xl shadow-2xl border border-slate-200/80 p-4 space-y-3 z-50 animate-fadeIn mt-1">
            <div class="flex justify-between items-center border-b border-slate-100 pb-2">
              <span class="font-bold text-xs font-serif text-slate-900">উইশলিস্ট ({{ wishlistItems.length }})</span>
              <NuxtLink to="/user/wishlist" class="text-[11px] text-rose-900 font-bold hover:underline">সব দেখুন</NuxtLink>
            </div>
            <div class="space-y-2 max-h-60 overflow-y-auto">
              <div v-for="item in wishlistItems" :key="item.id" class="flex items-center gap-3 p-2 rounded-xl bg-slate-50">
                <img :src="item.image" class="w-12 h-12 rounded-lg object-cover" alt="item" />
                <div class="flex-1 min-w-0">
                  <h4 class="text-xs font-bold font-serif text-slate-800 truncate">{{ item.title }}</h4>
                  <span class="text-xs font-extrabold text-rose-950">৳ {{ item.price }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- 2. Cart Dropdown Container -->
        <div class="relative" @mouseenter="isCartOpen = true" @mouseleave="isCartOpen = false">
          <NuxtLink to="/cart" class="relative p-2.5 bg-rose-900 text-white rounded-full hover:bg-rose-950 transition-colors flex items-center justify-center shadow-sm" aria-label="শপিং কার্ট">
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z"/>
            </svg>
            <span v-if="cartItems.length" class="absolute -top-1 -right-1 bg-amber-500 text-slate-950 text-xs font-bold w-5 h-5 rounded-full flex items-center justify-center border-2 border-white">
              {{ cartItems.length }}
            </span>
          </NuxtLink>

          <!-- Cart Animated Dropdown -->
          <div v-show="isCartOpen" class="absolute right-0 top-full w-80 sm:w-96 bg-white rounded-2xl shadow-2xl border border-slate-200/80 p-5 space-y-4 z-50 animate-fadeIn mt-1">
            <div class="flex justify-between items-center border-b border-slate-100 pb-3">
              <span class="font-bold text-sm font-serif text-slate-900">শপিং কার্ট ({{ cartItems.length }})</span>
              <span class="text-xs font-bold text-rose-900">৳ {{ cartSubtotal }}</span>
            </div>

            <div class="space-y-3 max-h-64 overflow-y-auto">
              <div v-for="item in cartItems" :key="item.id" class="flex items-center gap-3 p-2 rounded-xl bg-slate-50 border border-slate-100">
                <img :src="item.image" class="w-14 h-14 rounded-xl object-cover shrink-0" alt="cart item" />
                <div class="flex-1 min-w-0 space-y-0.5">
                  <h4 class="text-xs font-bold font-serif text-slate-900 truncate">{{ item.title }}</h4>
                  <p class="text-xs text-slate-500">পরিমাণ: {{ item.qty }}</p>
                  <span class="text-xs font-extrabold text-rose-950">৳ {{ item.price }}</span>
                </div>
              </div>
            </div>

            <div class="pt-2 border-t border-slate-100 space-y-2">
              <div class="flex justify-between items-center text-sm font-bold">
                <span class="text-slate-600">মোট সাবটোটাল:</span>
                <span class="text-rose-950">৳ {{ cartSubtotal }}</span>
              </div>
              <NuxtLink to="/cart" class="block text-center bg-rose-900 hover:bg-rose-950 text-white font-bold py-3 rounded-xl text-xs transition-colors shadow-md">
                চেকআউট করুন 🛍️
              </NuxtLink>
            </div>
          </div>
        </div>

        <!-- 3. Login / Register Account Buttons -->
        <div class="hidden lg:flex items-center gap-2 pl-2 border-l border-slate-200">
          <NuxtLink to="/login" class="px-4 py-2 rounded-xl text-xs font-bold text-slate-700 hover:bg-slate-100 transition-colors">
            লগইন
          </NuxtLink>
          <NuxtLink to="/register" class="px-4 py-2 rounded-xl text-xs font-bold bg-rose-900 text-white hover:bg-rose-950 transition-colors shadow-sm">
            রেজিস্ট্রেশন
          </NuxtLink>
        </div>

      </div>

    </div>
  </header>
</template>

<style scoped>
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(6px); }
  to { opacity: 1; transform: translateY(0); }
}
.animate-fadeIn {
  animation: fadeIn 0.2s ease-out forwards;
}
</style>