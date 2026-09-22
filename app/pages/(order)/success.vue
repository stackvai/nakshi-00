<!-- pages/checkout/success.vue -->
<script setup lang="ts">
useHead({
  title: 'অর্ডার সফল হয়েছে — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'আপনার অর্ডার সফলভাবে গৃহিত হয়েছে। অর্ডারের বিস্তারিত বিবরণ ও ট্র্যাকিং তথ্য।' }
  ]
})

// Mock completed order data
const orderDetails = {
  id: 'NK-9421',
  date: '২২ সেপ্টেম্বর, ২০২৬',
  paymentMethod: 'ক্যাশ অন ডেলিভারি (COD)',
  status: 'প্রক্রিয়াধীন',
  shippingAddress: {
    name: 'আবদুল বাসেত',
    phone: '01700000000',
    address: 'বাসা ১২, রোড ৩, ধানমন্ডি',
    district: 'ঢাকা'
  },
  items: [
    { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', price: 4500, qty: 1, size: 'ডাবল (৭ × ৮ ফুট)', image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=200' },
    { id: 3, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)', price: 1850, qty: 1, size: 'স্ট্যান্ডার্ড বেবি সাইজ', image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=200' }
  ],
  subtotal: 6350,
  deliveryFee: 120,
  total: 6470
}
</script>

<template>
  <div class="max-w-3xl mx-auto px-4 py-12 space-y-8">

    <!-- Top Success Banner -->
    <div class="bg-gradient-to-r from-rose-950 via-rose-900 to-slate-900 text-white rounded-3xl p-8 sm:p-10 text-center space-y-4 shadow-xl relative overflow-hidden">
      <div class="w-16 h-16 bg-emerald-500 text-white rounded-full flex items-center justify-center text-3xl mx-auto shadow-lg animate-bounce">
        ✓
      </div>
      <div class="space-y-1">
        <span class="bg-amber-400 text-slate-950 text-[10px] font-bold px-3 py-1 rounded-full uppercase tracking-widest">
          সফলভাবে সম্পন্ন
        </span>
        <h1 class="text-2xl sm:text-4xl font-bold font-serif">আপনার অর্ডারটি সফলভাবে গৃহিত হয়েছে!</h1>
        <p class="text-rose-100 text-xs sm:text-sm">
          অর্ডার আইডি: <strong class="text-amber-300">#{{ orderDetails.id }}</strong> | তারিখ: {{ orderDetails.date }}
        </p>
      </div>
    </div>

    <!-- Detailed Invoice & Information Grid -->
    <div class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-8 space-y-8 shadow-sm">
      
      <!-- Summary Cards (Address & Payment) -->
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 pb-6 border-b border-slate-100">
        
        <!-- Shipping Address -->
        <div class="bg-slate-50 p-5 rounded-2xl border border-slate-100 space-y-2">
          <h3 class="font-bold text-xs font-serif text-slate-900 uppercase tracking-wide flex items-center gap-1.5">
            <span>📍</span> ডেলিভারি ঠিকানা
          </h3>
          <div class="text-xs text-slate-600 space-y-1">
            <p class="font-bold text-slate-800">{{ orderDetails.shippingAddress.name }}</p>
            <p>ফোন: {{ orderDetails.shippingAddress.phone }}</p>
            <p>{{ orderDetails.shippingAddress.address }}, {{ orderDetails.shippingAddress.district }}</p>
          </div>
        </div>

        <!-- Payment & Status -->
        <div class="bg-slate-50 p-5 rounded-2xl border border-slate-100 space-y-2">
          <h3 class="font-bold text-xs font-serif text-slate-900 uppercase tracking-wide flex items-center gap-1.5">
            <span>💳</span> পেমেন্ট ও স্ট্যাটাস
          </h3>
          <div class="text-xs text-slate-600 space-y-1">
            <p>পেমেন্ট মাধ্যম: <strong class="text-slate-800">{{ orderDetails.paymentMethod }}</strong></p>
            <p>অর্ডার স্ট্যাটাস: <strong class="text-amber-700 bg-amber-100 px-2 py-0.5 rounded">{{ orderDetails.status }}</strong></p>
            <p>আনুমানিক ডেলিভারি: ৩ থেকে ৫ কার্যদিবস</p>
          </div>
        </div>

      </div>

      <!-- Ordered Items Breakdown Table -->
      <div class="space-y-4">
        <h3 class="font-bold text-sm font-serif text-slate-900">অর্ডারকৃত পণ্যের বিবরণ</h3>
        
        <div class="space-y-3">
          <div v-for="item in orderDetails.items" :key="item.id" class="flex items-center justify-between gap-4 p-3 rounded-2xl bg-slate-50 border border-slate-100">
            <div class="flex items-center gap-3">
              <img :src="item.image" class="w-12 h-12 rounded-xl object-cover shrink-0" alt="product" />
              <div>
                <h4 class="font-bold text-xs sm:text-sm font-serif text-slate-900">{{ item.title }}</h4>
                <p class="text-[11px] text-slate-500">সাইজ: {{ item.size }} | পরিমাণ: {{ item.qty }} টি</p>
              </div>
            </div>
            <span class="text-xs sm:text-sm font-extrabold text-rose-950 shrink-0">৳ {{ item.price * item.qty }}</span>
          </div>
        </div>
      </div>

      <!-- Financial Calculations -->
      <div class="bg-slate-50 p-5 rounded-2xl border border-slate-100 space-y-2 text-xs sm:text-sm text-slate-600">
        <div class="flex justify-between">
          <span>সাবটোটাল</span>
          <span class="font-bold text-slate-900">৳ {{ orderDetails.subtotal }}</span>
        </div>
        <div class="flex justify-between">
          <span>ডেলিভারি চার্জ</span>
          <span class="font-bold text-slate-900">৳ {{ orderDetails.deliveryFee }}</span>
        </div>
        <div class="flex justify-between items-center pt-3 border-t border-slate-200 text-base font-extrabold text-slate-900">
          <span>সর্বমোট প্রদেয়</span>
          <span class="text-rose-950 text-xl">৳ {{ orderDetails.total }}</span>
        </div>
      </div>

      <!-- Action Buttons -->
      <div class="pt-4 flex flex-col sm:flex-row gap-3">
        <NuxtLink to="/user/orders" class="flex-1 bg-rose-900 hover:bg-rose-950 text-white font-bold py-3.5 rounded-xl text-xs sm:text-sm text-center transition-colors shadow-md">
          আমার অর্ডারসমূহ দেখুন 📦
        </NuxtLink>
        <NuxtLink to="/shop" class="flex-1 bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold py-3.5 rounded-xl text-xs sm:text-sm text-center transition-colors">
          আরও কেনাকাটা করুন 🛍️
        </NuxtLink>
      </div>

    </div>

  </div>
</template>