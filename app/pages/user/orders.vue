<!-- pages/user/orders.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

definePageMeta({
  layout: 'user'
})

useHead({
  title: 'আমার অর্ডারসমূহ — নকশী কাঁথা স্টুডিও'
})

// Active tab switcher ('all' | 'active' | 'delivered')
const activeTab = ref('all')

// Mock orders database
const orders = ref([
  {
    id: 'NK-8921',
    date: '২১ সেপ্টেম্বর, ২০২৬',
    title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)',
    size: 'ডাবল (৭ × ৮ ফুট)',
    quantity: 1,
    price: 4500,
    status: 'শিপিং চলছে',
    statusCode: 'active',
    courier: 'Steadfast Courier (TRK-94821)'
  },
  {
    id: 'NK-8410',
    date: '১৫ আগস্ট, ২০২৬',
    title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)',
    size: 'স্ট্যান্ডার্ড বেবি সাইজ',
    quantity: 1,
    price: 1850,
    status: 'ডেলিভারি সম্পন্ন',
    statusCode: 'delivered',
    courier: 'RedX Express (DEL-11204)'
  },
  {
    id: 'NK-7902',
    date: '০২ জুলাই, ২০২৬',
    title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট',
    size: 'কিং সাইজ',
    quantity: 1,
    price: 3200,
    status: 'ডেলিভারি সম্পন্ন',
    statusCode: 'delivered',
    courier: 'Pathao Parcel (PTH-5510)'
  }
])

// Filtered orders based on active tab
const filteredOrders = computed(() => {
  if (activeTab.value === 'all') return orders.value
  return orders.value.filter(o => o.statusCode === activeTab.value)
})
</script>

<template>
  <div class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-8 space-y-6 shadow-sm">
    
    <!-- Header & Tab Navigation -->
    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 border-b border-slate-100 pb-5">
      <div>
        <h1 class="text-xl sm:text-2xl font-bold font-serif text-slate-900">আমার অর্ডারসমূহ</h1>
        <p class="text-xs text-slate-500 mt-0.5">আপনার সমস্ত কেনাকাটা ও শিপিং স্ট্যাটাস এখানে ট্র্যাক করুন</p>
      </div>

      <!-- Tab Buttons -->
      <div class="flex bg-slate-100 p-1 rounded-2xl border border-slate-200/60 w-full sm:w-auto">
        <button 
          @click="activeTab = 'all'"
          :class="['flex-1 sm:flex-none px-4 py-2 rounded-xl text-xs font-bold transition-all', activeTab === 'all' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-600 hover:text-slate-900']"
        >
          সব অর্ডার
        </button>
        <button 
          @click="activeTab = 'active'"
          :class="['flex-1 sm:flex-none px-4 py-2 rounded-xl text-xs font-bold transition-all', activeTab === 'active' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-600 hover:text-slate-900']"
        >
          চলমান
        </button>
        <button 
          @click="activeTab = 'delivered'"
          :class="['flex-1 sm:flex-none px-4 py-2 rounded-xl text-xs font-bold transition-all', activeTab === 'delivered' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-600 hover:text-slate-900']"
        >
          সম্পন্ন
        </button>
      </div>
    </div>

    <!-- Empty State -->
    <div v-if="filteredOrders.length === 0" class="text-center py-16 space-y-3">
      <span class="text-4xl">📦</span>
      <h3 class="font-bold text-base font-serif text-slate-800">কোনো অর্ডার পাওয়া যায়নি</h3>
      <p class="text-xs text-slate-500">আপনার এই ফিল্টারে কোনো অর্ডার রেকর্ড নেই।</p>
      <NuxtLink to="/shop" class="inline-block mt-2 bg-rose-900 text-white text-xs font-bold px-6 py-3 rounded-xl">
        শপ থেকে অর্ডার করুন 🛍️
      </NuxtLink>
    </div>

    <!-- Orders List -->
    <div v-else class="space-y-4">
      <div v-for="order in filteredOrders" :key="order.id" class="p-5 sm:p-6 rounded-2xl border border-slate-200/80 bg-slate-50/50 space-y-4 hover:border-rose-200 transition-colors">
        
        <!-- Top Order Info Bar -->
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2 border-b border-slate-200/60 pb-3">
          <div class="flex items-center gap-3">
            <span class="font-bold text-sm text-rose-950">{{ order.id }}</span>
            <span class="text-slate-300">•</span>
            <span class="text-xs text-slate-500">{{ order.date }}</span>
          </div>
          <div>
            <span :class="['text-xs font-bold px-3 py-1 rounded-full', order.statusCode === 'active' ? 'bg-amber-100 text-amber-900 border border-amber-200' : 'bg-emerald-100 text-emerald-900 border border-emerald-200']">
              {{ order.status }}
            </span>
          </div>
        </div>

        <!-- Product Details -->
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4">
          <div class="space-y-1">
            <h4 class="font-bold text-sm sm:text-base font-serif text-slate-900">{{ order.title }}</h4>
            <p class="text-xs text-slate-500">সাইজ: {{ order.size }} | পরিমাণ: {{ order.quantity }} টি</p>
            <p class="text-xs text-slate-400 font-medium pt-1">কুরিয়ার: {{ order.courier }}</p>
          </div>

          <div class="flex sm:flex-col justify-between items-center sm:items-end w-full sm:w-auto gap-3 pt-2 sm:pt-0 border-t sm:border-t-0 border-slate-200">
            <span class="text-base sm:text-lg font-extrabold text-rose-950">৳ {{ order.price }}</span>
            <div class="flex gap-2">
              <button class="bg-white hover:bg-slate-100 text-slate-700 border border-slate-200 text-xs font-bold px-3.5 py-2 rounded-xl transition-colors shadow-xs">
                ইনভয়েস 📄
              </button>
              <button class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-4 py-2 rounded-xl transition-colors shadow-xs">
                ট্রেস করুন 🚚
              </button>
            </div>
          </div>
        </div>

      </div>
    </div>

  </div>
</template>