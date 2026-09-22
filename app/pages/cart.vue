<!-- pages/cart.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

useHead({
  title: 'শপিং কার্ট — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'আপনার কার্টে যুক্ত থাকা পণ্যসমূহ দেখুন এবং চেকআউটের দিকে এগিয়ে যান।' }
  ]
})

// Reactive Cart Items State
const cartItems = ref([
  { 
    id: 1, 
    title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', 
    price: 4500, 
    originalPrice: 5200, 
    qty: 1, 
    size: 'ডাবল (৭ × ৮ ফুট)', 
    color: 'রাজকীয় মেরুন',
    image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' 
  },
  { 
    id: 3, 
    title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)', 
    price: 1850, 
    originalPrice: 2200, 
    qty: 1, 
    size: 'স্ট্যান্ডার্ড বেবি সাইজ', 
    color: 'সফট গোলাপি',
    image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' 
  }
])

const couponCode = ref('')
const discountAmount = ref(0)
const couponApplied = ref(false)
const couponMessage = ref('')

// Quantity adjustments
const increaseQty = (item: any) => {
  item.qty++
}

const decreaseQty = (item: any) => {
  if (item.qty > 1) {
    item.qty--
  }
}

const removeItem = (id: number) => {
  cartItems.value = cartItems.value.filter(i => i.id !== id)
}

// Subtotal calculations
const subtotal = computed(() => {
  return cartItems.value.reduce((acc, item) => acc + (item.price * item.qty), 0)
})

const deliveryFee = computed(() => {
  return cartItems.value.length > 0 ? 100 : 0
})

const finalTotal = computed(() => {
  return subtotal.value + deliveryFee.value - discountAmount.value
})

// Apply Coupon Action
const applyCoupon = () => {
  if (couponCode.value.toUpperCase() === 'WINTER500') {
    discountAmount.value = 500
    couponApplied.value = true
    couponMessage.value = '🎉 কুপন সফলভাবে প্রয়োগ করা হয়েছে (-৳ ৫০০)'
  } else {
    couponMessage.value = '❌ ভুল বা মেয়াদোত্তীর্ণ কুপন কোড!'
    couponApplied.value = false
  }
}
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-12 py-12">

    <!-- Breadcrumb -->
    <div class="text-xs text-slate-500 flex items-center gap-2">
      <NuxtLink to="/" class="hover:text-rose-900">হোম</NuxtLink>
      <span>/</span>
      <NuxtLink to="/shop" class="hover:text-rose-900">শপ</NuxtLink>
      <span>/</span>
      <span class="text-slate-900 font-medium">শপিং কার্ট</span>
    </div>

    <!-- Page Header -->
    <section class="text-center max-w-3xl mx-auto space-y-3">
      <span class="inline-block bg-rose-50 text-rose-900 border border-rose-200 text-xs font-bold px-4 py-1.5 rounded-full uppercase tracking-widest shadow-sm">
        আপনার শপিং ব্যাগ
      </span>
      <h1 class="text-3xl sm:text-5xl font-extrabold font-serif text-slate-900 leading-tight">
        শপিং কার্ট ({{ cartItems.length }} টি পণ্য)
      </h1>
    </section>

    <!-- Empty State -->
    <div v-if="cartItems.length === 0" class="text-center py-24 bg-white rounded-3xl border border-slate-200 space-y-4 shadow-sm max-w-2xl mx-auto">
      <span class="text-6xl">🛒</span>
      <h3 class="text-xl font-bold font-serif text-slate-900">আপনার কার্ট খালি রয়েছে!</h3>
      <p class="text-xs sm:text-sm text-slate-500">আমাদের কালেকশন থেকে আপনার পছন্দের প্রিমিয়াম নকশী কাঁথাটি কার্টে যোগ করুন।</p>
      <div class="pt-2">
        <NuxtLink to="/shop" class="inline-block bg-rose-900 hover:bg-rose-950 text-white font-bold px-8 py-3.5 rounded-xl text-sm transition-colors shadow-md">
          শপ ভিজিট করুন 🛍️
        </NuxtLink>
      </div>
    </div>

    <!-- Cart Layout (Table/List + Order Summary) -->
    <div v-else class="grid grid-cols-1 lg:grid-cols-3 gap-8 items-start">
      
      <!-- Left: Cart Items List -->
      <div class="lg:col-span-2 space-y-4">
        <div v-for="item in cartItems" :key="item.id" class="bg-white p-5 sm:p-6 rounded-3xl border border-slate-200/80 shadow-sm flex flex-col sm:flex-row items-center gap-6 group">
          
          <!-- Thumbnail -->
          <div class="w-full sm:w-32 aspect-[4/3] rounded-2xl overflow-hidden bg-slate-100 shrink-0">
            <img :src="item.image" class="w-full h-full object-cover" :alt="item.title" />
          </div>

          <!-- Details -->
          <div class="flex-1 space-y-1.5 text-center sm:text-left">
            <h3 class="font-bold text-base font-serif text-slate-900 group-hover:text-rose-900 transition-colors">
              {{ item.title }}
            </h3>
            <p class="text-xs text-slate-500">সাইজ: {{ item.size }} | কালার: {{ item.color }}</p>
            <div class="flex items-center justify-center sm:justify-start gap-2 pt-1">
              <span class="text-base font-extrabold text-rose-950">৳ {{ item.price }}</span>
              <span class="text-xs text-slate-400 line-through">৳ {{ item.originalPrice }}</span>
            </div>
          </div>

          <!-- Quantity Stepper & Remove -->
          <div class="flex sm:flex-col justify-between items-center sm:items-end w-full sm:w-auto gap-4 pt-3 sm:pt-0 border-t sm:border-t-0 border-slate-100">
            
            <div class="flex items-center border border-slate-200 rounded-xl bg-slate-50 overflow-hidden shadow-inner">
              <button @click="decreaseQty(item)" class="px-3 py-2 text-slate-600 hover:bg-slate-200 font-bold text-xs">−</button>
              <span class="px-3 text-xs font-bold text-slate-800">{{ item.qty }}</span>
              <button @click="increaseQty(item)" class="px-3 py-2 text-slate-600 hover:bg-slate-200 font-bold text-xs">+</button>
            </div>

            <button @click="removeItem(item.id)" class="text-xs text-rose-700 font-bold hover:underline flex items-center gap-1">
              🗑️ বাদ দিন
            </button>
          </div>

        </div>

        <!-- Continue Shopping Link -->
        <div class="pt-2">
          <NuxtLink to="/shop" class="text-xs font-bold text-rose-900 hover:underline flex items-center gap-1">
            ← আরও কেনাকাটা চালিয়ে যান
          </NuxtLink>
        </div>
      </div>

      <!-- Right: Order Summary Sidebar -->
      <div class="bg-white p-6 sm:p-8 rounded-3xl border border-slate-200/80 shadow-sm space-y-6 lg:col-span-1">
        <h3 class="text-lg font-bold font-serif text-slate-900 border-b border-slate-100 pb-3">অর্ডার সামারি</h3>

        <!-- Coupon Box -->
        <div class="space-y-2">
          <label class="text-xs font-bold text-slate-700">কুপন কোড আছে?</label>
          <div class="flex gap-2">
            <input 
              v-model="couponCode" 
              type="text" 
              placeholder="যেমন: WINTER500" 
              class="w-full px-3.5 py-2.5 rounded-xl border border-slate-200 text-xs focus:outline-none focus:border-rose-900 uppercase"
            />
            <button @click="applyCoupon" class="bg-slate-900 hover:bg-slate-950 text-white font-bold text-xs px-4 py-2.5 rounded-xl transition-colors shrink-0">
              প্রয়োগ
            </button>
          </div>
          <p v-if="couponMessage" :class="['text-[11px] font-bold mt-1', couponApplied ? 'text-emerald-700' : 'text-rose-700']">
            {{ couponMessage }}
          </p>
        </div>

        <!-- Calculation Breakdown -->
        <div class="space-y-3 pt-3 border-t border-slate-100 text-xs sm:text-sm text-slate-600">
          <div class="flex justify-between">
            <span>সাবটোটাল</span>
            <span class="font-bold text-slate-900">৳ {{ subtotal }}</span>
          </div>
          <div class="flex justify-between">
            <span>ডেলিভারি চার্জ (আনুমানিক)</span>
            <span class="font-bold text-slate-900">৳ {{ deliveryFee }}</span>
          </div>
          <div v-if="couponApplied" class="flex justify-between text-emerald-700 font-medium">
            <span>কুপন ডিসকাউন্ট</span>
            <span>-৳ {{ discountAmount }}</span>
          </div>
          <div class="flex justify-between items-center pt-3 border-t border-slate-100 text-base font-extrabold text-slate-900">
            <span>সর্বমোট প্রদেয়</span>
            <span class="text-rose-950 text-xl">৳ {{ finalTotal }}</span>
          </div>
        </div>

        <!-- Checkout Button -->
        <div class="pt-2">
          <NuxtLink to="/checkout" class="block w-full text-center bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-4 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99]">
            নিরাপদ চেকআউট করুন 🚀
          </NuxtLink>
        </div>

        <!-- Trust Badges -->
        <div class="grid grid-cols-3 gap-2 pt-2 text-center border-t border-slate-100">
          <div class="p-2 bg-slate-50 rounded-xl text-[10px] font-bold text-slate-600">📦 ক্যাশ অন ডেলিভারি</div>
          <div class="p-2 bg-slate-50 rounded-xl text-[10px] font-bold text-slate-600">🔒 নিরাপদ পেমেন্ট</div>
          <div class="p-2 bg-slate-50 rounded-xl text-[10px] font-bold text-slate-600">🌿 ১০০% অরিজিনাল</div>
        </div>

      </div>

    </div>

  </div>
</template>