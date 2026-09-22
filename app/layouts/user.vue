<!-- layouts/user.vue -->
<script setup lang="ts">
import { ref } from 'vue'

const isMobileMenuOpen = ref(false)

// User Account Navigation Links
const userNavLinks = [
  { label: 'ড্যাশবোর্ড ওভারভিউ', path: '/user', icon: '📊' },
  { label: 'আমার অর্ডারসমূহ', path: '/user/orders', icon: '📦' },
  { label: 'উইশলিস্ট ও পছন্দ', path: '/user/wishlist', icon: '❤️' },
  { label: 'ডেলিভারি ঠিকানা', path: '/user/addresses', icon: '📍' },
  { label: 'প্রোফাইল সেটিংস', path: '/user/settings', icon: '⚙️' }
]

const handleLogout = () => {
  // Clear user auth session here
  navigateTo('/login')
}
</script>

<template>
  <div class="min-h-screen bg-slate-100/70 flex flex-col font-sans text-slate-800">

    <!-- Top Navigation Bar (Mobile & Desktop Header) -->
    <header class="bg-white border-b border-slate-200 sticky top-0 z-50 px-4 sm:px-8 py-3.5 flex items-center justify-between shadow-xs">
      <div class="flex items-center gap-4">
        <button @click="isMobileMenuOpen = !isMobileMenuOpen" class="lg:hidden p-2 rounded-xl bg-slate-100 text-slate-700 font-bold hover:bg-slate-200 transition-colors">
          ☰
        </button>
        <NuxtLink to="/" class="font-serif font-extrabold text-lg text-rose-950 flex items-center gap-2">
          <span>🧵 নকশী কাঁথা স্টুডিও</span>
          <span class="text-[10px] font-sans bg-rose-50 text-rose-900 border border-rose-100 px-2.5 py-0.5 rounded-full font-bold uppercase tracking-wider hidden sm:inline">ইউজার পোর্টাল</span>
        </NuxtLink>
      </div>

      <div class="flex items-center gap-4">
        <NuxtLink to="/" class="text-xs font-bold text-slate-600 hover:text-rose-900 transition-colors hidden sm:inline">
          🏠 মূল ওয়েবসাইট
        </NuxtLink>
        <div class="flex items-center gap-2 bg-slate-50 border border-slate-200 px-3 py-1.5 rounded-2xl shadow-inner">
          <div class="w-7 h-7 rounded-full bg-rose-900 text-white font-bold flex items-center justify-center text-xs shadow-sm">
            AB
          </div>
          <span class="text-xs font-bold text-slate-700 hidden sm:inline">আবদুল বাসেত</span>
        </div>
      </div>
    </header>

    <!-- Main Two-Column Container -->
    <div class="max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 flex-1 grid grid-cols-1 lg:grid-cols-4 gap-8 items-start">
      
      <!-- LEFT SIDEBAR: Sticky Navigation & User Profile Card -->
      <aside :class="['lg:block space-y-6 lg:col-span-1 lg:sticky lg:top-24', isMobileMenuOpen ? 'fixed inset-y-0 left-0 z-50 w-80 bg-white shadow-2xl overflow-y-auto block p-6 pt-16 lg:pt-6' : 'hidden']">
        
        <!-- Mobile Close Button -->
        <div class="flex justify-between items-center lg:hidden border-b border-slate-100 pb-3">
          <span class="font-bold font-serif text-slate-900">ইউজার মেনু</span>
          <button @click="isMobileMenuOpen = false" class="text-slate-400 font-bold text-lg">✕</button>
        </div>

        <!-- Mini User Profile Box inside Sidebar -->
        <div class="bg-white p-5 rounded-3xl border border-slate-200/80 shadow-sm space-y-3 text-center">
          <div class="w-16 h-16 rounded-full bg-gradient-to-br from-rose-900 to-rose-950 text-white font-bold flex items-center justify-center text-xl mx-auto shadow-md">
            AB
          </div>
          <div>
            <h3 class="font-bold text-sm font-serif text-slate-900">আবদুল বাসেত</h3>
            <p class="text-xs text-slate-400 mt-0.5">bappy@example.com</p>
          </div>
          <div class="pt-2 border-t border-slate-100 flex justify-center gap-2">
            <span class="bg-amber-100 text-amber-900 text-[10px] font-bold px-2.5 py-0.5 rounded-full">মেম্বার</span>
            <span class="bg-emerald-100 text-emerald-900 text-[10px] font-bold px-2.5 py-0.5 rounded-full">ভেরিফাইড</span>
          </div>
        </div>

        <!-- Navigation Links Menu -->
        <div class="bg-white p-4 rounded-3xl border border-slate-200/80 shadow-sm space-y-1">
          <NuxtLink 
            v-for="link in userNavLinks" 
            :key="link.path" 
            :to="link.path"
            @click="isMobileMenuOpen = false"
            class="flex items-center gap-3 px-4 py-3 rounded-2xl text-xs sm:text-sm font-bold transition-all text-slate-700 hover:bg-rose-50 hover:text-rose-900"
            active-class="bg-rose-900 text-white hover:bg-rose-900 hover:text-white shadow-sm"
          >
            <span class="text-base">{{ link.icon }}</span>
            <span>{{ link.label }}</span>
          </NuxtLink>

          <div class="pt-3 mt-3 border-t border-slate-100">
            <button @click="handleLogout" class="w-full flex items-center gap-3 px-4 py-3 rounded-2xl text-xs sm:text-sm font-bold text-rose-700 hover:bg-rose-50 transition-colors">
              <span>🚪</span>
              <span>লগআউট করুন</span>
            </button>
          </div>
        </div>

      </aside>

      <!-- RIGHT MAIN CONTENT AREA -->
      <main class="lg:col-span-3 space-y-8">
        <slot />
      </main>

    </div>

  </div>
</template>