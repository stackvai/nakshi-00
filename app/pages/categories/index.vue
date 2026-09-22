<!-- pages/categories/index.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

useHead({
  title: 'সকল ক্যাটাগরি ও কালেকশন — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'জামালপুরের জিআই সনদপ্রাপ্ত ডাবল কাঁথা, সিঙ্গেল কাঁথা, বেবি কাঁথা ও নকশী বেডশীট ক্যাটাগরি সমূহ।' }
  ]
})

// Active category filter for live product preview preview
const selectedCategory = ref('double')

// Categories database with detailed descriptions and images
const categories = [
  {
    id: 'double',
    title: 'ডাবল নকশী কাঁথা',
    subtitle: 'শাহী ও ঐতিহ্যবাহী বড় সাইজের কাঁথা',
    count: '১২০+ পণ্য',
    image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=800',
    desc: '৭ × ৮ ফুট বা বড় আকৃতির এই কাঁথাগুলো শীতের উষ্ণতা এবং ঘরের আভিজাত্য বাড়াতে সেরা। শতভাগ হাতে সেলাই করা।'
  },
  {
    id: 'single',
    title: 'সিঙ্গেল কাঁথা',
    subtitle: 'একজনের ব্যবহারের জন্য উপযুক্ত',
    count: '৪৫+ পণ্য',
    image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=800',
    desc: 'দৈনন্দিন ব্যবহারের জন্য ৫ × ৭ ফুট মাপে নিখুঁত ফোঁড়ে তৈরি হালকা ও আরামদায়ক সিঙ্গেল কাঁথা।'
  },
  {
    id: 'baby',
    title: 'বেবি কাঁথা ও কম্বো সেট',
    subtitle: 'নবজাতকের কোমল ত্বকের সুরক্ষায়',
    count: '৪০+ পণ্য',
    image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=800',
    desc: '১০০% সফট প্রি-ওয়াশড সুতি কাপড় দিয়ে তৈরি, যা বেবিদের সংবেদনশীল ত্বকের জন্য সম্পূর্ণ নিরাপদ ও আরামদায়ক।'
  },
  {
    id: 'bedsheet',
    title: 'নকশী বেডশীট',
    subtitle: 'শোবার ঘরের সৌন্দর্য বর্ধনে',
    count: '৬৪+ পণ্য',
    image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=800',
    desc: 'ম্যাচিং কুশন কাভারসহ আকর্ষণীয় নকশী বেডশীট, যা আপনার বেডরুমকে দিবে রাজকীয় ও নান্দনিক লুক।'
  },
  {
    id: 'attire',
    title: 'হাতের কাজের থ্রি-পিস',
    subtitle: 'ঐতিহ্যবাহী পোশাক কালেকশন',
    count: '১৫০+ পণ্য',
    image: 'https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=800',
    desc: 'সুতি ও লিনেন কাপড়ের ওপর নিখুঁত হাতের সুতার কাজ করা চমৎকার সব থ্রি-পিস ও কুর্তি।'
  }
]

// Mock preview products corresponding to categories
const previewProducts = [
  { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', price: 4500, category: 'double', image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 2, title: 'ঐতিহ্যবাহী শাপলা কদম নকশী কাঁথা', price: 3800, category: 'double', image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 3, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)', price: 1850, category: 'baby', image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' },
  { id: 4, title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট', price: 3200, category: 'bedsheet', image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' },
  { id: 5, title: 'হাতে সেলাই করা সুতি নকশী তিন-পিস', price: 2450, category: 'attire', image: 'https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=600' },
  { id: 6, title: 'ভিক্টোরিয়ান লাল-হলুদ সিঙ্গেল কদম কাঁথা', price: 2750, category: 'single', image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' }
]

const filteredPreview = computed(() => {
  return previewProducts.filter(p => p.category === selectedCategory.value)
})
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-20 py-12">

    <!-- 1. Header Section -->
    <section class="text-center max-w-3xl mx-auto space-y-4">
      <span class="inline-block bg-amber-100 text-amber-900 border border-amber-200 text-xs font-bold px-4 py-1.5 rounded-full uppercase tracking-widest shadow-sm">
        পণ্যের ক্যাটাগরি
      </span>
      <h1 class="text-3xl sm:text-5xl font-extrabold font-serif text-slate-900 leading-tight">
        আপনার পছন্দের বিভাগ বেছে নিন
      </h1>
      <p class="text-slate-600 text-base sm:text-lg leading-relaxed">
        জামালপুরের শতবর্ষী জিআই সনদপ্রাপ্ত হস্তশিল্পের প্রতিটি ক্যাটাগরিতে রয়েছে নিখুঁত সুতোর বুনন ও আধুনিক নকশার সমাহার।
      </p>
    </section>

    <!-- 2. Categories Grid Showcase -->
    <section class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <div 
        v-for="cat in categories" 
        :key="cat.id" 
        @click="selectedCategory = cat.id"
        :class="[
          'group relative overflow-hidden rounded-3xl aspect-[4/3] cursor-pointer shadow-md transition-all duration-300 border-2',
          selectedCategory === cat.id ? 'border-rose-900 ring-4 ring-rose-900/10 scale-[1.02]' : 'border-slate-200/80 hover:border-rose-900/50'
        ]"
      >
        <img :src="cat.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700" :alt="cat.title" />
        <div class="absolute inset-0 bg-gradient-to-t from-slate-950/90 via-slate-950/30 to-transparent"></div>
        <div class="absolute bottom-0 p-6 sm:p-8 text-white space-y-2">
          <div class="flex items-center justify-between">
            <span class="inline-block bg-amber-500 text-slate-950 text-xs font-bold px-3 py-1 rounded-md">{{ cat.count }}</span>
            <span class="text-xs text-amber-300 font-medium group-hover:translate-x-1 transition-transform">দেখুন →</span>
          </div>
          <h3 class="text-xl sm:text-2xl font-bold font-serif">{{ cat.title }}</h3>
          <p class="text-xs sm:text-sm text-slate-300 line-clamp-1">{{ cat.subtitle }}</p>
        </div>
      </div>
    </section>

    <!-- 3. Live Preview Section for Selected Category -->
    <section class="bg-slate-50 p-8 sm:p-12 rounded-3xl border border-slate-200/80 space-y-8">
      <div class="flex flex-col sm:flex-row justify-between items-start sm:items-end gap-4 border-b border-slate-200 pb-4">
        <div>
          <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">সিলেক্টেড ক্যাটাগরি প্রিভিউ</span>
          <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 mt-1">নির্বাচিত বিভাগের সেরা পণ্যসমূহ</h2>
        </div>
        <NuxtLink to="/shop" class="bg-rose-900 hover:bg-rose-950 text-white font-bold text-xs px-5 py-2.5 rounded-xl transition-colors shadow-sm">
          শপে সব দেখুন 🛍️
        </NuxtLink>
      </div>

      <!-- Grid of Filtered Items -->
      <div v-if="filteredPreview.length > 0" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
        <div v-for="item in filteredPreview" :key="item.id" class="bg-white rounded-2xl border border-slate-200 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col justify-between group">
          <div>
            <div class="aspect-[4/3] overflow-hidden bg-slate-100">
              <img :src="item.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" :alt="item.title" />
            </div>
            <div class="p-4 space-y-2">
              <h3 class="font-bold text-sm text-slate-900 font-serif line-clamp-1 group-hover:text-rose-900 transition-colors">
                {{ item.title }}
              </h3>
            </div>
          </div>
          <div class="p-4 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
            <span class="text-base font-extrabold text-rose-950">৳ {{ item.price }}</span>
            <NuxtLink :to="`/products/${item.id}`" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-3.5 py-2 rounded-xl transition-colors">
              বিস্তারিত
            </NuxtLink>
          </div>
        </div>
      </div>

      <!-- Fallback if category preview is empty in mock -->
      <div v-else class="text-center py-12 bg-white rounded-2xl border border-slate-200 space-y-3">
        <span class="text-3xl">📦</span>
        <h4 class="font-bold text-base font-serif text-slate-800">এই ক্যাটাগরিতে নতুন পণ্য যুক্ত হচ্ছে</h4>
        <p class="text-xs text-slate-500">আমাদের ফুল শপ ভিজিট করে অন্যান্য চমৎকার ডিজাইন দেখে নিতে পারেন।</p>
        <NuxtLink to="/shop" class="inline-block mt-2 bg-rose-900 text-white text-xs font-bold px-5 py-2.5 rounded-xl">
          সব পণ্য দেখুন
        </NuxtLink>
      </div>
    </section>

    <!-- 4. Heritage & Custom Order Banner -->
    <section class="bg-rose-950 text-white rounded-3xl p-8 sm:p-14 text-center space-y-6 shadow-xl">
      <h2 class="text-2xl sm:text-4xl font-bold font-serif leading-snug">
        পছন্দের সাইজ বা কালার কম্বোতে কাঁথা বানাতে চান?
      </h2>
      <p class="text-rose-100 text-sm sm:text-base max-w-2xl mx-auto leading-relaxed">
        আমাদের রয়েছে কাস্টম অর্ডারের সুবিধা। আপনার পছন্দমতো মাপ, রঙ বা নকশা জানিয়ে দিলে জামালপুরের দক্ষ কারিগররা আপনার মনের মতো করে তৈরি করে দেবেন।
      </p>
      <div class="pt-2">
        <NuxtLink to="/contact" class="inline-block bg-amber-400 hover:bg-amber-300 text-slate-950 font-bold px-8 py-3.5 rounded-xl text-sm transition-colors shadow-lg">
          কাস্টম অর্ডারের জন্য কথা বলুন 📞
        </NuxtLink>
      </div>
    </section>

  </div>
</template>