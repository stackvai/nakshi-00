<!-- pages/blogs/index.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

useHead({
  title: 'ব্লগ ও ঐতিহ্যবাহী গল্প — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'জামালপুরের নকশী কাঁথার ইতিহাস, নারী কারিগরদের জীবনসংগ্রাম ও কাঁথার সঠিক যত্ন নিয়ে আমাদের ব্লগ পোস্টসমূহ।' }
  ]
})

const activeCategory = ref('all')

const categories = [
  { id: 'all', label: 'সকল লেখা' },
  { id: 'heritage', label: 'ঐতিহ্য ও ইতিহাস' },
  { id: 'artisan', label: 'কারিগরদের গল্প' },
  { id: 'care', label: 'যত্ন ও পরিচর্যা' }
]

// Blog database
const posts = [
  {
    id: 1,
    title: 'জামালপুরের নকশী কাঁথার জিআই (GI) স্বীকৃতি ও আমাদের শেকড়ের গল্প',
    slug: 'jamalpur-nakshi-katha-gi-certification',
    category: 'heritage',
    categoryLabel: 'ঐতিহ্য ও ইতিহাস',
    date: '১৮ সেপ্টেম্বর, ২০২৬',
    readTime: '৪ মিনিট পঠন',
    excerpt: 'বাংলাদেশের লোকশিল্পের ইতিহাসে জামালপুরের নকশী কাঁথার ভৌগোলিক নির্দেশক বা জিআই সনদপ্রাপ্তির গৌরবোজ্জ্বল ইতিহাস ও এর পেছনের দীর্ঘ পথচলা।',
    image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=800',
    featured: true
  },
  {
    id: 2,
    title: 'রেহানা বেগমের গল্প: কুঁড়েঘরের বারান্দা থেকে বিশ্বদরবারে',
    slug: 'artisan-rehana-begum-story',
    category: 'artisan',
    categoryLabel: 'কারিগরদের গল্প',
    date: '১০ সেপ্টেম্বর, ২০২৬',
    readTime: '৫ মিনিট পঠন',
    excerpt: 'মেলান্দহের প্রান্তিক নারী কারিগর রেহানা বেগমের হাতের জাদুকরী ফোঁড় কীভাবে তার পরিবারের ভাগ্য বদলে দিয়েছে এবং তাকে স্বাবলম্বী করেছে।',
    image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600',
    featured: false
  },
  {
    id: 3,
    title: 'শীতের রাতে ওমের ছোঁয়া: কীভাবে নেবেন আপনার নকশী কাঁথার সঠিক যত্ন?',
    slug: 'how-to-care-for-nakshi-katha',
    category: 'care',
    categoryLabel: 'যত্ন ও পরিচর্যা',
    date: '২৫ আগস্ট, ২০২৬',
    readTime: '৩ মিনিট পঠন',
    excerpt: 'শতভাগ প্রি-ওয়াশড সুতি কাপড় ও পাকা রঙের সুতো দিয়ে তৈরি নকশী কাঁথা দীর্ঘদিন নতুনের মতো টিকিয়ে রাখতে কিছু সহজ ওয়াশ কেয়ার টিপস।',
    image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600',
    featured: false
  },
  {
    id: 4,
    title: 'নকশী কাঁথার মোটিফ ও নকশার পেছনের সুপ্ত অর্থ',
    slug: 'nakshi-katha-motifs-and-meanings',
    category: 'heritage',
    categoryLabel: 'ঐতিহ্য ও ইতিহাস',
    date: '১২ আগস্ট, ২০২৬',
    readTime: '৬ মিনিট পঠন',
    excerpt: 'শাপলা, কদম ফুল, ময়ূরপঙ্খী নৌকা এবং লতা-পাতার মোটিফগুলোতে গ্রামীণ নারীরা কীভাবে তাদের মনের সুপ্ত স্বপ্ন ও প্রকৃতির রূপ ফুটিয়ে তোলেন।',
    image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600',
    featured: false
  }
]

const filteredPosts = computed(() => {
  if (activeCategory.value === 'all') return posts
  return posts.filter(p => p.category === activeCategory.value)
})

const featuredPost = computed(() => {
  return posts.find(p => p.featured) || posts[0]
})
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-16 py-12">

    <!-- 1. Header Section -->
    <section class="text-center max-w-3xl mx-auto space-y-4">
      <span class="inline-block bg-rose-50 text-rose-900 border border-rose-200 text-xs font-bold px-4 py-1.5 rounded-full uppercase tracking-widest shadow-sm">
        নকশী ব্লগ ও গল্প
      </span>
      <h1 class="text-3xl sm:text-5xl font-extrabold font-serif text-slate-900 leading-tight">
        লোকশিল্প, ঐতিহ্য ও সুতোর ফোঁড়ের গল্প
      </h1>
      <p class="text-slate-600 text-base sm:text-lg leading-relaxed">
        জামালপুরের হস্তশিল্পের ইতিহাস, কারিগরদের জীবনসংগ্রাম এবং আমাদের ঐতিহ্য নিয়ে জানতে পড়ুন আমাদের ব্লগসমূহ।
      </p>
    </section>

    <!-- 2. Featured Hero Blog Post -->
    <section v-if="activeCategory === 'all' || activeCategory === featuredPost.category" class="bg-rose-950 text-white rounded-3xl overflow-hidden shadow-xl grid lg:grid-cols-2 gap-8 items-center">
      <div class="aspect-[16/10] lg:aspect-auto h-full overflow-hidden">
        <img :src="featuredPost.image" class="w-full h-full object-cover hover:scale-105 transition-transform duration-700" alt="Featured Post" />
      </div>
      <div class="p-8 sm:p-12 space-y-4">
        <div class="flex items-center gap-3 text-xs">
          <span class="bg-amber-500 text-slate-950 font-bold px-3 py-1 rounded-md">{{ featuredPost.categoryLabel }}</span>
          <span class="text-rose-200">{{ featuredPost.date }}</span>
          <span class="text-rose-300">•</span>
          <span class="text-rose-200">{{ featuredPost.readTime }}</span>
        </div>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif leading-snug hover:text-amber-300 transition-colors cursor-pointer">
          {{ featuredPost.title }}
        </h2>
        <p class="text-rose-100/90 text-sm leading-relaxed">
          {{ featuredPost.excerpt }}
        </p>
        <div class="pt-2">
          <NuxtLink :to="`/blogs/${featuredPost.slug}`" class="inline-block bg-amber-400 hover:bg-amber-300 text-slate-950 font-bold text-xs px-6 py-3 rounded-xl transition-colors shadow-md">
            সম্পূর্ণ পড়ুন →
          </NuxtLink>
        </div>
      </div>
    </section>

    <!-- 3. Category Filter Tabs -->
    <section class="flex justify-center flex-wrap gap-2 pt-4">
      <button
        v-for="cat in categories"
        :key="cat.id"
        @click="activeCategory = cat.id"
        :class="[
          'px-5 py-2.5 rounded-xl font-medium text-xs sm:text-sm transition-all shadow-sm',
          activeCategory === cat.id ? 'bg-rose-900 text-white shadow-md' : 'bg-white text-slate-700 hover:bg-slate-100 border border-slate-200'
        ]"
      >
        {{ cat.label }}
      </button>
    </section>

    <!-- 4. Blog Posts Grid -->
    <section class="space-y-8">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="post in filteredPosts" :key="post.id" class="bg-white rounded-3xl border border-slate-200/80 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col justify-between group">
          <div>
            <div class="aspect-[16/10] overflow-hidden bg-slate-100 relative">
              <span class="absolute top-4 left-4 z-10 bg-rose-900 text-white text-[11px] font-bold px-3 py-1 rounded shadow-sm">
                {{ post.categoryLabel }}
              </span>
              <img :src="post.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" :alt="post.title" />
            </div>
            <div class="p-6 space-y-3">
              <div class="flex items-center gap-2 text-xs text-slate-400">
                <span>{{ post.date }}</span>
                <span>•</span>
                <span>{{ post.readTime }}</span>
              </div>
              <h3 class="font-bold text-lg text-slate-900 font-serif leading-snug group-hover:text-rose-900 transition-colors">
                {{ post.title }}
              </h3>
              <p class="text-xs sm:text-sm text-slate-600 line-clamp-2 leading-relaxed">
                {{ post.excerpt }}
              </p>
            </div>
          </div>
          <div class="p-6 pt-0">
            <NuxtLink :to="`/blogs/${post.slug}`" class="text-xs font-bold text-rose-900 hover:text-rose-950 underline flex items-center gap-1">
              বিস্তারিত পড়ুন <span>→</span>
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>