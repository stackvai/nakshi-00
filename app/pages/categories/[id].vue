<!-- pages/categories/[id].vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const categoryId = String(route.params.id) || 'double'

// Category metadata mapping
const categoryMeta: Record<string, { title: string; subtitle: string; desc: string }> = {
  double: {
    title: 'ডাবল নকশী কাঁথা কালেকশন',
    subtitle: 'শাহী ও ঐতিহ্যবাহী বড় সাইজের কাঁথা',
    desc: '৭ × ৮ ফুট বা বড় আকৃতির এই কাঁথাগুলো শীতের উষ্ণতা এবং ঘরের আভিজাত্য বাড়াতে সেরা। শতভাগ হাতে সেলাই করা।'
  },
  single: {
    title: 'সিঙ্গেল কাঁথা কালেকশন',
    subtitle: 'একজনের ব্যবহারের জন্য উপযুক্ত',
    desc: 'দৈনন্দিন ব্যবহারের জন্য ৫ × ৭ ফুট মাপে নিখুঁত ফোঁড়ে তৈরি হালকা ও আরামদায়ক সিঙ্গেল কাঁথা।'
  },
  baby: {
    title: 'বেবি কাঁথা ও কম্বো সেট',
    subtitle: 'নবজাতকের কোমল ত্বকের সুরক্ষায়',
    desc: '১০০% সফট প্রি-ওয়াশড সুতি কাপড় দিয়ে তৈরি, যা বেবিদের সংবেদনশীল ত্বকের জন্য সম্পূর্ণ নিরাপদ ও আরামদায়ক।'
  },
  bedsheet: {
    title: 'নকশী বেডশীট কালেকশন',
    subtitle: 'শোবার ঘরের সৌন্দর্য বর্ধনে',
    desc: 'ম্যাচিং কুশন কাভারসহ আকর্ষণীয় নকশী বেডশীট, যা আপনার বেডরুমকে দিবে রাজকীয় ও নান্দনিক লুক।'
  },
  attire: {
    title: 'হাতের কাজের থ্রি-পিস কালেকশন',
    subtitle: 'ঐতিহ্যবাহী পোশাক কালেকশন',
    desc: 'সুতি ও লিনেন কাপড়ের ওপর নিখুঁত হাতের সুতার কাজ করা চমৎকার সব থ্রি-পিস ও কুর্তি।'
  }
}

const currentCategory = computed(() => {
  return categoryMeta[categoryId] || {
    title: 'ক্যাটাগরি পণ্যসমূহ',
    subtitle: 'জামালপুরের হস্তশিল্প',
    desc: 'আমাদের শতভাগ হাতে তৈরি প্রিমিয়াম কালেকশন।'
  }
})

// Filter & Sort State
const selectedTag = ref('all')
const searchQuery = ref('')
const sortBy = ref('featured')
const maxPrice = ref(6000)
const viewMode = ref<'grid' | 'list'>('grid')
const selectedProduct = ref<any>(null)

// Full Product Database with category tags
const products = [
  { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', price: 4500, originalPrice: 5200, category: 'double', tag: 'হট সেলিং', rating: 5.0, reviews: 48, image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 2, title: 'ঐতিহ্যবাহী শাপলা কদম নকশী কাঁথা', price: 3800, originalPrice: 4200, category: 'double', tag: 'জিআই সার্টিফাইড', rating: 4.9, reviews: 32, image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 3, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)', price: 1850, originalPrice: 2200, category: 'baby', tag: 'সফট কটন', rating: 5.0, reviews: 29, image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' },
  { id: 4, title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট', price: 3200, originalPrice: 3700, category: 'bedsheet', tag: 'পাকা রং', rating: 4.8, reviews: 19, image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' },
  { id: 5, title: 'হাতে সেলাই করা সুতি নকশী তিন-পিস', price: 2450, originalPrice: 2900, category: 'attire', tag: 'নতুন ডিজাইন', rating: 4.9, reviews: 54, image: 'https://images.unsplash.com/photo-1610030469983-98e550d6193c?q=80&w=600' },
  { id: 6, title: 'ভিক্টোরিয়ান লাল-হলুদ সিঙ্গেল কদম কাঁথা', price: 2750, originalPrice: 3100, category: 'single', tag: 'জনপ্রিয়', rating: 4.7, reviews: 21, image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 7, title: 'মাদারগঞ্জ স্পেশাল ফ্লাওয়ার নকশী কাঁথা', price: 4100, originalPrice: 4600, category: 'double', tag: 'জিআই সার্টিফাইড', rating: 4.9, reviews: 15, image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' },
  { id: 8, title: 'মেলান্দহ ক্লাসিক মাস্টারপিস কাঁথা', price: 4900, originalPrice: 5500, category: 'double', tag: 'মাস্টারপিস', rating: 5.0, reviews: 27, image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' },
  { id: 9, title: 'নবজাতকের রঙিন সুতি কুশন ও কাঁথা সেট', price: 1450, originalPrice: 1750, category: 'baby', tag: 'বেবি স্পেশাল', rating: 4.8, reviews: 12, image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 10, title: 'হাতে বোনা মিনি বেবি নকশী কাঁথা', price: 950, originalPrice: 1200, category: 'baby', tag: 'সেরা দাম', rating: 4.7, reviews: 33, image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600' }
]

const tags = ['all', 'হট সেলিং', 'জিআই সার্টিফাইড', 'সফট কটন', 'পাকা রং', 'নতুন ডিজাইন', 'মাস্টারপিস']

const resetFilters = () => {
  selectedTag.value = 'all'
  searchQuery.value = ''
  maxPrice.value = 6000
  sortBy.value = 'featured'
}

// Filter products strictly by current route category + secondary filters
const filteredProducts = computed(() => {
  let result = products.filter(p => p.category === categoryId)

  if (selectedTag.value !== 'all') {
    result = result.filter(p => p.tag === selectedTag.value)
  }

  result = result.filter(p => p.price <= maxPrice.value)

  if (searchQuery.value.trim() !== '') {
    const q = searchQuery.value.toLowerCase()
    result = result.filter(p => p.title.toLowerCase().includes(q))
  }

  if (sortBy.value === 'low-high') {
    result = [...result].sort((a, b) => a.price - b.price)
  } else if (sortBy.value === 'high-low') {
    result = [...result].sort((a, b) => b.price - a.price)
  } else if (sortBy.value === 'rating') {
    result = [...result].sort((a, b) => b.rating - a.rating)
  }

  return result
})
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-12 py-12">

    <!-- Breadcrumb -->
    <div class="text-xs text-slate-500 flex items-center gap-2">
      <NuxtLink to="/" class="hover:text-rose-900">হোম</NuxtLink>
      <span>/</span>
      <NuxtLink to="/categories" class="hover:text-rose-900">ক্যাটাগরি</NuxtLink>
      <span>/</span>
      <span class="text-slate-900 font-medium">{{ currentCategory.title }}</span>
    </div>

    <!-- 1. Category Banner Header -->
    <section class="bg-gradient-to-br from-rose-950 via-rose-900 to-slate-900 text-white rounded-3xl p-8 sm:p-14 space-y-4 shadow-xl relative overflow-hidden">
      <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#d97706_1px,transparent_1px)] [background-size:16px_16px]"></div>
      <div class="max-w-2xl space-y-3 relative z-10">
        <span class="bg-amber-400 text-slate-950 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-wider">
          {{ currentCategory.subtitle }}
        </span>
        <h1 class="text-3xl sm:text-5xl font-extrabold font-serif leading-tight">
          {{ currentCategory.title }}
        </h1>
        <p class="text-rose-100 text-sm sm:text-base leading-relaxed">
          {{ currentCategory.desc }}
        </p>
      </div>
    </section>

    <!-- 2. Search & Top Control Bar -->
    <section class="bg-white p-5 sm:p-6 rounded-3xl border border-slate-200 shadow-sm flex flex-col md:flex-row justify-between items-center gap-4">
      
      <!-- Live Search Box -->
      <div class="relative w-full md:w-96">
        <input 
          v-model="searchQuery" 
          type="text" 
          placeholder="এই ক্যাটাগরিতে খুঁজুন..." 
          class="w-full px-4 py-3 pl-11 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
        />
        <span class="absolute left-4 top-3.5 text-slate-400">🔍</span>
      </div>

      <!-- Controls: Sorting & Grid View Switcher -->
      <div class="flex items-center gap-3 w-full md:w-auto justify-between md:justify-end">
        <div class="flex items-center gap-2">
          <span class="text-xs font-bold text-slate-500 whitespace-nowrap hidden sm:inline">সাজিয়ে নিন:</span>
          <select 
            v-model="sortBy" 
            class="px-4 py-3 rounded-xl bg-slate-50 border border-slate-200 text-xs sm:text-sm focus:outline-none focus:border-rose-900 shadow-sm cursor-pointer"
          >
            <option value="featured">ফিচারড বা সেরা</option>
            <option value="low-high">মূল্য: কম থেকে বেশি</option>
            <option value="high-low">মূল্য: বেশি থেকে কম</option>
            <option value="rating">সর্বোচ্চ রেটিং</option>
          </select>
        </div>

        <div class="flex items-center gap-1 bg-slate-100 p-1 rounded-xl border border-slate-200">
          <button @click="viewMode = 'grid'" :class="['p-2 rounded-lg text-xs font-bold transition-colors', viewMode === 'grid' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-500']">🔲 গ্রিড</button>
          <button @click="viewMode = 'list'" :class="['p-2 rounded-lg text-xs font-bold transition-colors', viewMode === 'list' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-500']">📋 লিস্ট</button>
        </div>
      </div>
    </section>

    <!-- 3. Main Layout: Filters + Products Grid -->
    <section class="grid grid-cols-1 lg:grid-cols-4 gap-8 items-start">
      
      <!-- Sidebar Filters -->
      <aside class="space-y-8 bg-white p-6 sm:p-8 rounded-3xl border border-slate-200 shadow-sm lg:col-span-1">
        
        <!-- Price Range Filter Slider -->
        <div class="space-y-4">
          <h3 class="font-bold text-sm font-serif text-slate-900 border-b border-slate-100 pb-2">
            💰 সর্বোচ্চ মূল্য সীমা
          </h3>
          <div class="space-y-3">
            <div class="flex justify-between items-center text-xs font-bold text-slate-700">
              <span>৳ ০</span>
              <span class="text-rose-900 bg-rose-50 px-2.5 py-1 rounded-lg border border-rose-100">৳ {{ maxPrice }}</span>
            </div>
            <input 
              v-model.number="maxPrice" 
              type="range" 
              min="500" 
              max="6000" 
              step="100" 
              class="w-full accent-rose-900 cursor-pointer"
            />
          </div>
        </div>

        <!-- Tag Filters -->
        <div class="space-y-4">
          <h3 class="font-bold text-sm font-serif text-slate-900 border-b border-slate-100 pb-2">
            🏷️ বিশেষ বৈশিষ্ট্য
          </h3>
          <div class="flex flex-wrap gap-1.5">
            <button
              v-for="tag in tags"
              :key="tag"
              @click="selectedTag = tag"
              :class="[
                'px-3 py-1.5 rounded-xl text-xs transition-all font-medium',
                selectedTag === tag ? 'bg-rose-900 text-white font-bold' : 'bg-slate-100 text-slate-700 hover:bg-slate-200'
              ]"
            >
              {{ tag === 'all' ? 'সকল ট্যাগ' : tag }}
            </button>
          </div>
        </div>

        <!-- Reset Button -->
        <div class="pt-2">
          <button @click="resetFilters" class="w-full bg-slate-100 hover:bg-slate-200 text-slate-700 font-bold text-xs py-3 rounded-xl transition-colors">
            🔄 ফিল্টার রিসেট করুন
          </button>
        </div>

      </aside>

      <!-- Products Display Area -->
      <div class="lg:col-span-3 space-y-6">
        
        <!-- Results Info -->
        <div class="flex justify-between items-center text-xs sm:text-sm text-slate-500 bg-white p-4 rounded-2xl border border-slate-200">
          <span>এই ক্যাটাগরিতে মোট <strong class="text-slate-900">{{ filteredProducts.length }}</strong> টি পণ্য পাওয়া গেছে</span>
        </div>

        <!-- Empty State -->
        <div v-if="filteredProducts.length === 0" class="text-center py-24 bg-white rounded-3xl border border-slate-200 space-y-4 shadow-sm">
          <span class="text-5xl">📦</span>
          <h3 class="text-lg font-bold font-serif text-slate-800">এই ফিল্টারের সাথে মিলে এমন কোনো পণ্য নেই</h3>
          <p class="text-xs text-slate-500">অনুগ্রহ করে মূল্য সীমা বাড়ান অথবা ফিল্টার রিসেট করুন।</p>
          <button @click="resetFilters" class="mt-2 bg-rose-900 text-white font-bold text-xs px-6 py-3 rounded-xl shadow-md">
            সব ফিল্টার রিসেট করুন
          </button>
        </div>

        <!-- Grid View -->
        <div v-else-if="viewMode === 'grid'" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-for="product in filteredProducts" :key="product.id" class="bg-white rounded-2xl border border-slate-200/80 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col justify-between group">
            <div>
              <div class="relative aspect-[4/3] overflow-hidden bg-slate-100">
                <span v-if="product.tag" class="absolute top-3 left-3 z-10 bg-rose-900 text-white text-xs font-bold px-2.5 py-1 rounded shadow-sm">
                  {{ product.tag }}
                </span>
                <img :src="product.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" :alt="product.title" />
              </div>
              <div class="p-4 space-y-2">
                <div class="flex items-center justify-between text-xs">
                  <span class="text-amber-500 font-bold">★ {{ product.rating }}</span>
                  <span class="text-slate-400">({{ product.reviews }} রিভিউ)</span>
                </div>
                <h3 class="font-bold text-sm text-slate-800 font-serif line-clamp-1 group-hover:text-rose-900 transition-colors">
                  {{ product.title }}
                </h3>
              </div>
            </div>
            
            <div class="p-4 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
              <div>
                <span class="text-base font-extrabold text-rose-950">৳ {{ product.price }}</span>
                <span class="text-xs text-slate-400 line-through ml-1.5">৳ {{ product.originalPrice }}</span>
              </div>
              <NuxtLink :to="`/products/${product.id}`" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-3.5 py-2 rounded-xl transition-colors shadow-sm">
                বিস্তারিত
              </NuxtLink>
            </div>
          </div>
        </div>

        <!-- List View -->
        <div v-else class="space-y-4">
          <div v-for="product in filteredProducts" :key="product.id" class="bg-white rounded-2xl border border-slate-200/80 p-4 sm:p-5 flex flex-col sm:flex-row items-center gap-6 shadow-sm hover:shadow-md transition-all group">
            <div class="w-full sm:w-40 aspect-[4/3] rounded-xl overflow-hidden bg-slate-100 relative shrink-0">
              <span v-if="product.tag" class="absolute top-2 left-2 z-10 bg-rose-900 text-white text-[10px] font-bold px-2 py-0.5 rounded">
                {{ product.tag }}
              </span>
              <img :src="product.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" :alt="product.title" />
            </div>
            <div class="flex-1 space-y-2 text-center sm:text-left">
              <div class="flex items-center justify-center sm:justify-start gap-2 text-xs">
                <span class="text-amber-500 font-bold">★ {{ product.rating }}</span>
                <span class="text-slate-400">• ({{ product.reviews }} রিভিউ)</span>
              </div>
              <h3 class="font-bold text-base text-slate-900 font-serif group-hover:text-rose-900 transition-colors">
                {{ product.title }}
              </h3>
              <p class="text-xs text-slate-500">জামালপুরের শতভাগ হাতে সেলাই করা প্রিমিয়াম মানের জিআই সনদপ্রাপ্ত হস্তশিল্প।</p>
            </div>
            <div class="flex sm:flex-col justify-between items-center sm:items-end w-full sm:w-auto gap-3 pt-3 sm:pt-0 border-t sm:border-t-0 border-slate-100">
              <div>
                <span class="text-lg font-extrabold text-rose-950">৳ {{ product.price }}</span>
                <span class="text-xs text-slate-400 line-through ml-2">৳ {{ product.originalPrice }}</span>
              </div>
              <NuxtLink :to="`/products/${product.id}`" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-5 py-2.5 rounded-xl transition-colors shadow-sm">
                বিস্তারিত 🛒
              </NuxtLink>
            </div>
          </div>
        </div>

      </div>

    </section>

  </div>
</template>