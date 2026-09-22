<!-- pages/user/index.vue -->
<script setup lang="ts">
definePageMeta({
  layout: 'user'
})

useHead({
  title: 'ইউজার ড্যাশবোর্ড — নকশী কাঁথা স্টুডিও'
})

// Mock recent orders for logged-in user
const recentOrders = [
  { id: 'NK-8921', date: '২১ সেপ্টেম্বর, ২০২৬', title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা', price: 4500, status: 'শিপিং চলছে' },
  { id: 'NK-8410', date: '১৫ আগস্ট, ২০২৬', title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো', price: 1850, status: 'ডেলিভারি সম্পন্ন' }
]
</script>

<template>
  <div class="space-y-8">

    <!-- Welcome Banner -->
    <div class="bg-gradient-to-r from-rose-900 to-rose-950 text-white rounded-3xl p-6 sm:p-8 space-y-2 shadow-lg">
      <span class="bg-amber-400 text-slate-950 text-[10px] font-bold px-2.5 py-1 rounded-full uppercase">ভেরিফাইড অ্যাকাউন্ট</span>
      <h1 class="text-2xl sm:text-3xl font-bold font-serif">স্বাগতম, আবদুল বাসেত!</h1>
      <p class="text-rose-100 text-xs sm:text-sm">আপনার বর্তমান অর্ডার স্ট্যাটাস, উইশলিস্ট ও ঠিকানা এখান থেকে ম্যানেজ করুন।</p>
    </div>

    <!-- Quick Stats Metric Cards -->
    <div class="grid grid-cols-2 sm:grid-cols-4 gap-4">
      <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm space-y-1">
        <span class="text-xs text-slate-400 font-medium">মোট অর্ডার</span>
        <h3 class="text-2xl font-bold font-serif text-slate-900">০৪ টি</h3>
      </div>
      <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm space-y-1">
        <span class="text-xs text-slate-400 font-medium">চলমান শিপমেন্ট</span>
        <h3 class="text-2xl font-bold font-serif text-rose-900">০১ টি</h3>
      </div>
      <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm space-y-1">
        <span class="text-xs text-slate-400 font-medium">উইশলিস্ট পণ্য</span>
        <h3 class="text-2xl font-bold font-serif text-slate-900">০৩ টি</h3>
      </div>
      <div class="bg-white p-5 rounded-2xl border border-slate-200/80 shadow-sm space-y-1">
        <span class="text-xs text-slate-400 font-medium">লয়্যালটি পয়েন্ট</span>
        <h3 class="text-2xl font-bold font-serif text-amber-600">৩৫০ পিটি</h3>
      </div>
    </div>

    <!-- Recent Orders Table Section -->
    <div class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-8 space-y-6 shadow-sm">
      <div class="flex justify-between items-center border-b border-slate-100 pb-4">
        <h2 class="text-lg sm:text-xl font-bold font-serif text-slate-900">সাম্প্রতিক অর্ডারসমূহ</h2>
        <NuxtLink to="/user/orders" class="text-xs font-bold text-rose-900 hover:underline">সব দেখুন →</NuxtLink>
      </div>

      <div class="space-y-4">
        <div v-for="order in recentOrders" :key="order.id" class="p-4 rounded-2xl bg-slate-50 border border-slate-100 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
          <div class="space-y-1">
            <div class="flex items-center gap-2">
              <span class="text-xs font-bold text-rose-900">{{ order.id }}</span>
              <span class="text-slate-300">•</span>
              <span class="text-xs text-slate-400">{{ order.date }}</span>
            </div>
            <h4 class="font-bold text-sm text-slate-800 font-serif">{{ order.title }}</h4>
          </div>

          <div class="flex items-center justify-between w-full sm:w-auto gap-4 pt-2 sm:pt-0 border-t sm:border-t-0 border-slate-200">
            <span class="text-sm font-extrabold text-rose-950">৳ {{ order.price }}</span>
            <span :class="['text-xs font-bold px-3 py-1 rounded-full', order.status === 'শিপিং চলছে' ? 'bg-amber-100 text-amber-900' : 'bg-emerald-100 text-emerald-900']">
              {{ order.status }}
            </span>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>