<!-- pages/products/[id].vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const productId = Number(route.params.id) || 1

// Mock database of products (in real app, fetch based on productId)
const product = ref({
  id: productId,
  title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)',
  price: 4500,
  originalPrice: 5200,
  rating: 5.0,
  reviewsCount: 48,
  category: 'double',
  tag: 'হট সেলিং',
  sku: 'NK-SHAHI-01',
  description: 'জামালপুরের প্রবীণ ও দক্ষ নারী কারিগরদের শতভাগ নিজ হাতে সেলাই করা শাহী ময়ূরপঙ্খী নকশী কাঁথা। এটি প্রি-ওয়াশড শতভাগ নরম সুতি কাপড় ও পাকা রঙে তৈরি, যা শীতের ওমে এবং ঘরের সৌন্দর্য বাড়াতে অনন্য।',
  images: [
    'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=800',
    'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=800',
    'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=800'
  ]
})

const activeImage = ref(product.value.images[0])
const selectedSize = ref('ডাবল (৭ × ৮ ফুট)')
const selectedColor = ref('রাজকীয় মেরুন')
const quantity = ref(1)
const activeTab = ref('description')
const addedToCart = ref(false)

const sizes = ['ডাবল (৭ × ৮ ফুট)', 'সিঙ্গেল (৫ × ৭ ফুট)', 'কিং সাইজ (৮ × ৯ ফুট)']
const colors = ['রাজকীয় মেরুন', 'ঐতিহ্যবাহী নীল', 'শাহী লাল', 'সবুজ কদম']

const handleAddToCart = () => {
  addedToCart.value = true
  setTimeout(() => {
    addedToCart.value = false
  }, 3000)
}

// Related Products
const relatedProducts = [
  { id: 2, title: 'ঐতিহ্যবাহী শাপলা কদম নকশী কাঁথা', price: 3800, originalPrice: 4200, image: 'https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600' },
  { id: 3, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো', price: 1850, originalPrice: 2200, image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=600' },
  { id: 4, title: 'রাজকীয় নীল অল-ওভার নকশী বেডশীট', price: 3200, originalPrice: 3700, image: 'https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=600' }
]
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-20 py-12">

    <!-- Breadcrumb -->
    <div class="text-xs text-slate-500 flex items-center gap-2">
      <NuxtLink to="/" class="hover:text-rose-900">হোম</NuxtLink>
      <span>/</span>
      <NuxtLink to="/shop" class="hover:text-rose-900">শপ</NuxtLink>
      <span>/</span>
      <span class="text-slate-900 font-medium truncate">{{ product.title }}</span>
    </div>

    <!-- 1. Main Product Section -->
    <section class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-start">
      
      <!-- Left: Image Gallery -->
      <div class="space-y-4">
        <div class="aspect-[4/3] rounded-3xl overflow-hidden bg-slate-100 border border-slate-200/80 shadow-sm relative">
          <span v-if="product.tag" class="absolute top-4 left-4 z-10 bg-rose-900 text-white text-xs font-bold px-3 py-1 rounded-md shadow">
            {{ product.tag }}
          </span>
          <img :src="activeImage" class="w-full h-full object-cover transition-all duration-300" alt="Product Preview" />
        </div>
        <div class="grid grid-cols-3 gap-4">
          <button 
            v-for="(img, i) in product.images" 
            :key="i"
            @click="activeImage = img"
            :class="['aspect-[4/3] rounded-2xl overflow-hidden border-2 transition-all', activeImage === img ? 'border-rose-900 scale-95 shadow-md' : 'border-slate-200 opacity-70 hover:opacity-100']"
          >
            <img :src="img" class="w-full h-full object-cover" alt="Thumbnail" />
          </button>
        </div>
      </div>

      <!-- Right: Product Info & Actions -->
      <div class="space-y-6">
        
        <div class="space-y-2">
          <div class="flex items-center gap-2 text-xs">
            <span class="bg-amber-100 text-amber-900 font-bold px-2.5 py-0.5 rounded">★ {{ product.rating }}</span>
            <span class="text-slate-400">({{ product.reviewsCount }} টি কাস্টমার রিভিউ)</span>
            <span class="text-slate-300">|</span>
            <span class="text-slate-500">কোড: {{ product.sku }}</span>
          </div>
          <h1 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900 leading-snug">
            {{ product.title }}
          </h1>
        </div>

        <!-- Price Tag -->
        <div class="flex items-baseline gap-3 pt-2 border-t border-slate-100">
          <span class="text-3xl font-extrabold text-rose-950">৳ {{ product.price }}</span>
          <span class="text-sm text-slate-400 line-through">৳ {{ product.originalPrice }}</span>
          <span class="text-xs font-bold bg-emerald-50 text-emerald-800 px-2.5 py-1 rounded-md border border-emerald-200">
            সাশ্রয়ী মূল্য
          </span>
        </div>

        <p class="text-sm text-slate-600 leading-relaxed">
          {{ product.description }}
        </p>

        <!-- Size Selector -->
        <div class="space-y-3 pt-2">
          <label class="text-xs font-bold text-slate-700 uppercase tracking-wide">সাইজ নির্বাচন করুন:</label>
          <div class="flex flex-wrap gap-2">
            <button 
              v-for="size in sizes" 
              :key="size"
              @click="selectedSize = size"
              :class="['px-4 py-2 rounded-xl text-xs sm:text-sm font-medium transition-all border', selectedSize === size ? 'bg-rose-900 text-white border-rose-900 shadow-sm' : 'bg-white text-slate-700 border-slate-200 hover:bg-slate-50']"
            >
              {{ size }}
            </button>
          </div>
        </div>

        <!-- Color Selector -->
        <div class="space-y-3">
          <label class="text-xs font-bold text-slate-700 uppercase tracking-wide">কালার নির্বাচন করুন:</label>
          <div class="flex flex-wrap gap-2">
            <button 
              v-for="color in colors" 
              :key="color"
              @click="selectedColor = color"
              :class="['px-4 py-2 rounded-xl text-xs sm:text-sm font-medium transition-all border', selectedColor === color ? 'bg-rose-900 text-white border-rose-900 shadow-sm' : 'bg-white text-slate-700 border-slate-200 hover:bg-slate-50']"
            >
              {{ color }}
            </button>
          </div>
        </div>

        <!-- Quantity & Add to Cart -->
        <div class="space-y-4 pt-4 border-t border-slate-100">
          <div class="flex items-center gap-4">
            <div class="flex items-center border border-slate-200 rounded-2xl bg-white overflow-hidden shadow-inner">
              <button @click="quantity > 1 ? quantity-- : null" class="px-4 py-3 text-slate-600 hover:bg-slate-100 font-bold">−</button>
              <span class="px-4 text-sm font-bold text-slate-800">{{ quantity }}</span>
              <button @click="quantity++" class="px-4 py-3 text-slate-600 hover:bg-slate-100 font-bold">+</button>
            </div>
            
            <button 
              @click="handleAddToCart"
              class="flex-1 bg-rose-900 hover:bg-rose-950 text-white font-bold py-3.5 px-6 rounded-2xl text-sm transition-all shadow-lg shadow-rose-950/10 active:scale-[0.99] flex items-center justify-center gap-2"
            >
              <span>কার্টে যোগ করুন 🛒</span>
            </button>
          </div>

          <!-- Success Feedback Alert -->
          <div v-if="addedToCart" class="p-3 bg-emerald-50 border border-emerald-200 text-emerald-800 text-xs rounded-xl flex items-center gap-2">
            <span>✅</span> সফলভাবে কার্টে যুক্ত হয়েছে!
          </div>
        </div>

        <!-- Value Proposition Badges -->
        <div class="grid grid-cols-3 gap-3 pt-4 border-t border-slate-100 text-center">
          <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
            <span class="block text-lg">📦</span>
            <span class="text-[11px] font-bold text-slate-700 mt-1 block">ক্যাশ অন ডেলিভারি</span>
          </div>
          <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
            <span class="block text-lg">🌿</span>
            <span class="text-[11px] font-bold text-slate-700 mt-1 block">১০০% প্রিমিয়াম সুতি</span>
          </div>
          <div class="p-3 bg-slate-50 rounded-xl border border-slate-100">
            <span class="block text-lg">🎖️</span>
            <span class="text-[11px] font-bold text-slate-700 mt-1 block">জিআই সার্টিফাইড</span>
          </div>
        </div>

      </div>
    </section>

    <!-- 2. Detailed Navigation Tabs (Description, Artisan, Authenticity, Care, FAQ) -->
    <section class="bg-white rounded-3xl border border-slate-200/80 p-6 sm:p-10 shadow-sm space-y-8">
      
      <!-- Tab Switcher Buttons -->
      <div class="flex flex-wrap gap-2 border-b border-slate-200 pb-4">
        <button 
          @click="activeTab = 'desc'" 
          :class="['px-5 py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', activeTab === 'desc' ? 'bg-rose-900 text-white shadow-md' : 'bg-slate-100 text-slate-700 hover:bg-slate-200']"
        >
          📄 পণ্যের বিবরণ
        </button>
        <button 
          @click="activeTab = 'artisan'" 
          :class="['px-5 py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', activeTab === 'artisan' ? 'bg-rose-900 text-white shadow-md' : 'bg-slate-100 text-slate-700 hover:bg-slate-200']"
        >
          👩‍🎨 কারিগর ও তৈরির প্রক্রিয়া
        </button>
        <button 
          @click="activeTab = 'authenticity'" 
          :class="['px-5 py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', activeTab === 'authenticity' ? 'bg-rose-900 text-white shadow-md' : 'bg-slate-100 text-slate-700 hover:bg-slate-200']"
        >
          🛡️ সত্যতা ও জিআই (QR Code)
        </button>
        <button 
          @click="activeTab = 'care'" 
          :class="['px-5 py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', activeTab === 'care' ? 'bg-rose-900 text-white shadow-md' : 'bg-slate-100 text-slate-700 hover:bg-slate-200']"
        >
          🧺 ব্যবহারের নির্দেশাবলী
        </button>
        <button 
          @click="activeTab = 'faq'" 
          :class="['px-5 py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', activeTab === 'faq' ? 'bg-rose-900 text-white shadow-md' : 'bg-slate-100 text-slate-700 hover:bg-slate-200']"
        >
          ❓ আরও প্রশ্ন ও উত্তর
        </button>
      </div>

      <!-- Tab Content Area -->
      <div class="text-slate-700 text-sm leading-relaxed">
        
        <!-- Tab 1: Description -->
        <div v-if="activeTab === 'desc'" class="space-y-4 animate-fadeIn">
          <h3 class="font-serif text-lg font-bold text-slate-900">পণ্যের বিস্তারিত বিবরণ</h3>
          <p>
            জামালপুরের ঐতিহ্যবাহী ও শতভাগ হস্তশিল্পে তৈরি এই নকশী কাঁথাটি আপনার শোবার ঘরে নিয়ে আসবে আভিজাত্য ও উষ্ণতার ছোঁয়া। এর প্রতিটি ফোঁড়ে ফুটিয়ে তোলা হয়েছে গ্রামীণ লোকশিল্পের অনন্য কারুকার্য।
          </p>
          <ul class="list-disc list-inside space-y-1.5 text-slate-600">
            <li><strong>উপাদান:</strong> ১০০% প্রি-ওয়াশড সফট সুতি কাপড় ও পাকা সুতো।</li>
            <li><strong>সাইজ:</strong> ডাবল বেডের জন্য ৭ × ৮ ফুট।</li>
            <li><strong>তৈরির সময়:</strong> একটি কাঁথা তৈরি করতে দক্ষ কারিগরদের ৭ থেকে ১০ দিন সময় লাগে।</li>
          </ul>
        </div>

        <!-- Tab 2: Artisan & Process -->
        <div v-else-if="activeTab === 'artisan'" class="space-y-4 animate-fadeIn">
          <h3 class="font-serif text-lg font-bold text-slate-900">কারিগর ও তৈরির প্রক্রিয়া</h3>
          <p>
            আমাদের প্রতিটি কাঁথা জামালপুরের মেলান্দহ ও মাদারগঞ্জ উপজেলার গ্রামীণ নারীদের নিপুণ হাতে সেলাই করা। পুরুষানুক্রমে চলে আসা এই লোকশিল্পের মাধ্যমে গ্রামীণ নারীরা স্বাবলম্বী হচ্ছেন।
          </p>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2">
            <div class="p-4 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
              <span class="font-bold text-rose-900">১. সুতি কাপড় নির্বাচন</span>
              <p class="text-xs text-slate-500">উচ্চমানের নরম সুতি কাপড় একাধিক স্তরে সাজানো হয়।</p>
            </div>
            <div class="p-4 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
              <span class="font-bold text-rose-900">২. সূচ ও ফোঁড়ের কাজ</span>
              <p class="text-xs text-slate-500">হাতের নিখুঁত ফোঁড়ে লতা-পাতা ও ময়ূরপঙ্খী মোটিফ ফুটিয়ে তোলা হয়।</p>
            </div>
            <div class="p-4 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
              <span class="font-bold text-rose-900">৩. ফিনিশিং ও ওয়াশ</span>
              <p class="text-xs text-slate-500">চূড়ান্ত মান যাচাই শেষে প্রি-ওয়াশ করে ডেলিভারির জন্য প্রস্তুত করা হয়।</p>
            </div>
          </div>
        </div>

        <!-- Tab 3: Authenticity & QR Code (Origin & GI) -->
        <div v-else-if="activeTab === 'authenticity'" class="space-y-6 animate-fadeIn">
          <div class="flex flex-col md:flex-row items-center gap-8 bg-rose-50/50 p-6 sm:p-8 rounded-3xl border border-rose-100">
            <div class="bg-white p-4 rounded-2xl border border-slate-200 shadow-sm shrink-0 text-center space-y-2">
              <img :src="product.qrCodeUrl" class="w-32 h-32 mx-auto" alt="Authenticity QR Code" />
              <span class="text-[10px] font-mono text-slate-500 block">SCAN FOR GI VERIFICATION</span>
            </div>

            <div class="space-y-3">
              <span class="bg-rose-900 text-white text-xs font-bold px-3 py-1 rounded-md">
                জিআই সনদপ্রাপ্ত (GI Certified)
              </span>
              <h3 class="font-serif text-xl font-bold text-slate-900">শতভাগ অরিজিনাল জামালপুরি হস্তশিল্প</h3>
              <p class="text-xs sm:text-sm text-slate-600">
                এই পণ্যটির উৎপত্তিস্থল ও মূল উৎস হলো: <strong class="text-rose-950">{{ product.origin }}</strong>। উপরের QR কোডটি স্ক্যান করে আপনি সরাসরি জামালপুর হস্তশিল্প সমবায় সংঘের ডিজিটাল ডাটাবেজ থেকে এর অরিজিনালিটি ও কারিগরের স্বাক্ষর যাচাই করতে পারবেন।
              </p>
              <div class="text-xs text-slate-500 pt-1">
                📌 অ্যাসোসিয়েশন: <strong>{{ product.artisanGroup }}</strong>
              </div>
            </div>
          </div>
        </div>

        <!-- Tab 4: Washing & Care Instructions -->
        <div v-else-if="activeTab === 'care'" class="space-y-4 animate-fadeIn">
          <h3 class="font-serif text-lg font-bold text-slate-900">ব্যবহার ও যত্নের নির্দেশাবলী</h3>
          <p>আপনার শখের নকশী কাঁথাটি দীর্ঘদিন নতুনের মতো টিকিয়ে রাখতে নিচের নিয়মগুলো অনুসরণ করুন:</p>
          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="p-4 rounded-2xl bg-amber-50/50 border border-amber-100 space-y-1">
              <span class="font-bold text-amber-900">💧 ধোয়ার নিয়ম</span>
              <p class="text-xs text-slate-600">হালকা কুসুম গরম পানি ও মাইল্ড ডিটারজেন্ট দিয়ে হাত দিয়ে মৃদুভাবে ধোবেন। মেশিনে কাচবেন না।</p>
            </div>
            <div class="p-4 rounded-2xl bg-amber-50/50 border border-amber-100 space-y-1">
              <span class="font-bold text-amber-900">☀️ শুকানোর নিয়ম</span>
              <p class="text-xs text-slate-600">সরাসরি তীব্র রোদে না শুকিয়ে ছায়াযুক্ত বাতাসে শুকালে রঙের উজ্জ্বলতা চিরস্থায়ী থাকে।</p>
            </div>
          </div>
        </div>

        <!-- Tab 5: FAQs -->
        <div v-else-if="activeTab === 'faq'" class="space-y-4 animate-fadeIn">
          <h3 class="font-serif text-lg font-bold text-slate-900">সাধারণ জিজ্ঞাসা (FAQ)</h3>
          <div class="space-y-3">
            <div class="p-4 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
              <h4 class="font-bold text-sm text-slate-800">প্রোডাক্ট কি ছবি বা ভিডিওর সাথে হুবহু মিলবে?</h4>
              <p class="text-xs text-slate-600">হ্যাঁ, আমাদের নিজস্ব কারিগরদের তৈরি অরিজিনাল পণ্যের ছবি দেওয়া হয়েছে। তবে হাতের কাজের কারণে সুতার রঙে সামান্য ভিন্নতা থাকতে পারে।</p>
            </div>
            <div class="p-4 rounded-2xl bg-slate-50 border border-slate-100 space-y-1">
              <h4 class="font-bold text-sm text-slate-800">ডেলিভারির সময় কি পার্সেল চেক করা যাবে?</h4>
              <p class="text-xs text-slate-600">অবশ্যই! আমাদের ক্যাশ অন ডেলিভারি অর্ডারে কুরিয়ার ম্যানের সামনে পণ্য চেক করে বুঝে নেওয়ার সুযোগ রয়েছে।</p>
            </div>
          </div>
        </div>

      </div>
    </section>

    <!-- 3. Related Products Section -->
    <section class="space-y-6">
      <div class="border-b border-slate-100 pb-4">
        <h2 class="text-2xl font-bold font-serif text-slate-900">আপনার পছন্দ হতে পারে এমন আরও পণ্য</h2>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-3 gap-6">
        <div v-for="item in relatedProducts" :key="item.id" class="bg-white rounded-2xl border border-slate-200/80 overflow-hidden shadow-sm hover:shadow-md transition-all flex flex-col justify-between group">
          <div>
            <div class="aspect-[4/3] overflow-hidden bg-slate-100">
              <img :src="item.image" class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500" alt="Related" />
            </div>
            <div class="p-4 space-y-2">
              <h3 class="font-bold text-sm text-slate-800 font-serif line-clamp-1 group-hover:text-rose-900 transition-colors">
                {{ item.title }}
              </h3>
            </div>
          </div>
          <div class="p-4 pt-0 flex items-center justify-between border-t border-slate-50 mt-2">
            <span class="text-base font-extrabold text-rose-950">৳ {{ item.price }}</span>
            <NuxtLink :to="`/products/${item.id}`" class="bg-rose-900 hover:bg-rose-950 text-white text-xs font-bold px-3 py-1.5 rounded-lg transition-colors">
              বিস্তারিত দেখুন
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

  </div>
</template>