<!-- components/layout/SubHeader.vue -->
<script setup lang="ts">
import { ref } from 'vue'

const isMegaMenuOpen = ref(false)

const megaCategories = [
  { name: 'ডাবল সাইজ নকশী কাঁথা', path: '/categories/double', icon: '🛏️', desc: 'শাহী ও বড় আকৃতির কাঁথা' },
  { name: 'প্রিমিয়াম সিঙ্গেল কাঁথা', path: '/categories/single', icon: '🛋️', desc: 'হালকা ও আরামদায়ক সিঙ্গেল' },
  { name: 'বেবি নকশী কাঁথা কম্বো', path: '/categories/baby', icon: '👶', desc: 'নবজাতকদের জন্য সফট কটন' },
  { name: 'হাতে সেলাইয়ের বেডশীট', path: '/categories/bedsheet', icon: '✨', desc: 'কুশন কাভারসহ বেডরুম সেট' },
  { name: 'হাতের কাজের থ্রি-পিস', path: '/categories/attire', icon: '👗', desc: 'ঐতিহ্যবাহী সুতি থ্রি-পিস' }
]

const navLinks = [
  { name: 'সকল শপ', path: '/shop' },
  { name: 'আমাদের গল্প', path: '/about' },
  { name: 'ব্লগ ও ঐতিহ্য', path: '/blogs' },
  { name: 'যোগাযোগ', path: '/contact' },
  { name: 'অফার ও ডিসকাউন্ট', path: '/offers', highlight: true }
]
</script>

<template>
  <nav class="bg-rose-900 text-white shadow-md hidden md:block relative z-30">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <ul class="flex items-center justify-between text-sm font-medium py-1">
        
        <!-- Left Side: Mega Menu Dropdown Trigger -->
        <li class="relative" @mouseenter="isMegaMenuOpen = true" @mouseleave="isMegaMenuOpen = false">
          <button 
            @click="isMegaMenuOpen = !isMegaMenuOpen"
            class="flex items-center gap-2 px-4 py-2.5 rounded-xl bg-rose-950/80 text-amber-300 font-bold hover:bg-rose-950 transition-colors shadow-inner cursor-pointer"
          >
            <span>📂 সকল ক্যাটাগরি (মেগা মেনু)</span>
            <span class="text-xs transition-transform duration-300" :class="isMegaMenuOpen ? 'rotate-180' : ''">▼</span>
          </button>

          <!-- Mega Menu Flyout Panel -->
          <div 
            v-show="isMegaMenuOpen" 
            class="absolute top-full left-0 w-[420px] bg-white text-slate-900 rounded-2xl shadow-2xl border border-slate-200/80 p-4 grid grid-cols-1 gap-2 animate-fadeIn mt-1"
          >
            <div class="text-[11px] font-bold text-slate-400 uppercase tracking-wider px-3 pt-1">জনপ্রিয় ক্যাটাগরি সমূহ</div>
            <NuxtLink 
              v-for="cat in megaCategories" 
              :key="cat.path"
              :to="cat.path"
              @click="isMegaMenuOpen = false"
              class="flex items-center gap-3.5 p-3 rounded-xl hover:bg-rose-50 transition-colors group"
            >
              <span class="w-10 h-10 rounded-xl bg-rose-100 text-rose-900 flex items-center justify-center text-lg group-hover:bg-rose-900 group-hover:text-white transition-colors">
                {{ cat.icon }}
              </span>
              <div>
                <h4 class="font-bold text-sm text-slate-800 font-serif group-hover:text-rose-900">{{ cat.name }}</h4>
                <p class="text-xs text-slate-500">{{ cat.desc }}</p>
              </div>
            </NuxtLink>
            
            <div class="pt-2 border-t border-slate-100 mt-1 text-center">
              <NuxtLink to="/categories" @click="isMegaMenuOpen = false" class="text-xs font-bold text-rose-900 hover:underline">
                সব ক্যাটাগরি একসাথে দেখুন →
              </NuxtLink>
            </div>
          </div>
        </li>

        <!-- Right Side: Important Navigation Links -->
        <div class="flex items-center gap-1 overflow-x-auto py-1">
          <li v-for="link in navLinks" :key="link.path">
            <NuxtLink
              :to="link.path"
              class="block px-4 py-2.5 rounded-lg whitespace-nowrap transition-colors hover:bg-rose-950/60"
              :class="link.highlight ? 'text-amber-300 font-semibold' : 'text-rose-50'"
              active-class="bg-rose-950 text-white font-semibold"
            >
              {{ link.name }}
            </NuxtLink>
          </li>
        </div>

      </ul>
    </div>
  </nav>
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