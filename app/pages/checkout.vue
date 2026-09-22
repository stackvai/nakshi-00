<!-- pages/checkout.vue -->
<script setup lang="ts">
import { ref, computed } from 'vue'

useHead({
  title: 'চেকআউট ও অর্ডার কনফার্মেশন — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'আপনার শিপিং ঠিকানা ও পেমেন্ট পদ্ধতি নির্বাচন করে অর্ডার কনফার্ম করুন।' }
  ]
})

// Checkout Form State
const form = ref({
  fullName: '',
  phone: '',
  email: '',
  district: 'জামালপুর',
  address: '',
  note: '',
  paymentMethod: 'cod' // 'cod' or 'online'
})

const isSubmitting = ref(false)
const errorMessage = ref('')

// Mock cart items summary (can be linked to global state)
const cartItems = ref([
  { id: 1, title: 'জামালপুরি শাহী ময়ূরপঙ্খী নকশী কাঁথা (ডাবল)', price: 4500, qty: 1, image: 'https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=200' },
  { id: 3, title: 'কোমল তুলতুলে বেবি নকশী কাঁথা কম্বো (৩ পিস)', price: 1850, qty: 1, image: 'https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=200' }
])

const subtotal = computed(() => {
  return cartItems.value.reduce((acc, item) => acc + (item.price * item.qty), 0)
})

const deliveryFee = computed(() => {
  return form.value.district === 'ঢাকা' ? 120 : 100
})

const finalTotal = computed(() => {
  return subtotal.value + deliveryFee.value
})

const handlePlaceOrder = () => {
  errorMessage.value = ''

  if (!form.value.fullName || !form.value.phone || !form.value.address) {
    errorMessage.value = 'দয়া করে নাম, মোবাইল নম্বর এবং সম্পূর্ণ ঠিকানা লিখুন।'
    return
  }

  isSubmitting.value = true
  setTimeout(() => {
    isSubmitting.value = false
    navigateTo('/checkout/success')
  }, 1500)
}
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-12 py-12">

    <!-- Breadcrumb -->
    <div class="text-xs text-slate-500 flex items-center gap-2">
      <NuxtLink to="/" class="hover:text-rose-900">হোম</NuxtLink>
      <span>/</span>
      <NuxtLink to="/cart" class="hover:text-rose-900">কার্ট</NuxtLink>
      <span>/</span>
      <span class="text-slate-900 font-medium">চেকআউট</span>
    </div>

    <!-- Page Header -->
    <section class="text-center max-w-3xl mx-auto space-y-3">
      <span class="inline-block bg-rose-50 text-rose-900 border border-rose-200 text-xs font-bold px-4 py-1.5 rounded-full uppercase tracking-widest shadow-sm">
        নিরাপদ চেকআউট
      </span>
      <h1 class="text-3xl sm:text-5xl font-extrabold font-serif text-slate-900 leading-tight">
        আপনার শিপিং ও পেমেন্ট তথ্য দিন
      </h1>
    </section>

    <!-- Error Alert -->
    <div v-if="errorMessage" class="max-w-3xl mx-auto p-4 bg-rose-50 border border-rose-200 text-rose-800 text-xs rounded-2xl text-center font-bold shadow-sm">
      ⚠️ {{ errorMessage }}
    </div>

    <!-- Checkout Grid -->
    <form @submit.prevent="handlePlaceOrder" class="grid grid-cols-1 lg:grid-cols-3 gap-8 items-start">
      
      <!-- Left: Shipping & Payment Details Form -->
      <div class="lg:col-span-2 space-y-8">
        
        <!-- 1. Shipping Details Box -->
        <div class="bg-white p-6 sm:p-8 rounded-3xl border border-slate-200/80 shadow-sm space-y-6">
          <h2 class="text-xl font-bold font-serif text-slate-900 border-b border-slate-100 pb-3 flex items-center gap-2">
            <span>📍</span> ১. ডেলিভারি ঠিকানা
          </h2>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="space-y-1.5">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">আপনার পূর্ণ নাম *</label>
              <input v-model="form.fullName" type="text" required placeholder="যেমন: আবদুল বাসেত" class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
            </div>
            <div class="space-y-1.5">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">মোবাইল নম্বর *</label>
              <input v-model="form.phone" type="tel" required placeholder="01XXXXXXXXX" class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
            </div>
          </div>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            <div class="space-y-1.5">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">ইমেইল (ঐচ্ছিক)</label>
              <input v-model="form.email" type="email" placeholder="example@gmail.com" class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
            </div>
            <div class="space-y-1.5">
              <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">জেলা নির্বাচন করুন *</label>
              <select v-model="form.district" class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner cursor-pointer">
                <option value="জামালপুর">জামালপুর</option>
                <option value="ঢাকা">ঢাকা</option>
                <option value="চট্টগ্রাম">চট্টগ্রাম</option>
                <option value="সিলেট">সিলেট</option>
                <option value="রাজশাহী">রাজশাহী</option>
                <option value="খুলনা">খুলনা</option>
                <option value="অন্যান্য">অন্যান্য জেলা</option>
              </select>
            </div>
          </div>

          <div class="space-y-1.5">
            <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">সম্পূর্ণ ঠিকানা (বাসা, রোড, এলাকা) *</label>
            <textarea v-model="form.address" rows="3" required placeholder="যেমন: বাসা ১২, রোড ৩, ধানমন্ডি" class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner resize-none"></textarea>
          </div>

          <div class="space-y-1.5">
            <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">ডেলিভারি নির্দেশিকা (যদি থাকে)</label>
            <input v-model="form.note" type="text" placeholder="যেমন: বিকালে কল করবেন" class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner" />
          </div>
        </div>

        <!-- 2. Payment Method Box -->
        <div class="bg-white p-6 sm:p-8 rounded-3xl border border-slate-200/80 shadow-sm space-y-6">
          <h2 class="text-xl font-bold font-serif text-slate-900 border-b border-slate-100 pb-3 flex items-center gap-2">
            <span>💳</span> ২. পেমেন্ট পদ্ধতি
          </h2>

          <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
            
            <!-- COD Option -->
            <label :class="['p-5 rounded-2xl border-2 cursor-pointer transition-all flex items-start gap-3', form.paymentMethod === 'cod' ? 'border-rose-900 bg-rose-50/40 shadow-sm' : 'border-slate-200 bg-slate-50/50 hover:border-slate-300']">
              <input v-model="form.paymentMethod" type="radio" value="cod" class="mt-1 accent-rose-900" />
              <div class="space-y-1">
                <span class="font-bold text-sm text-slate-900 font-serif block">ক্যাশ অন ডেলিভারি (COD)</span>
                <p class="text-xs text-slate-500">পণ্য হাতে পেয়ে পার্সেল চেক করে কুরিয়ার ম্যানকে পেমেন্ট করুন।</p>
              </div>
            </label>

            <!-- Online Payment Option -->
            <label :class="['p-5 rounded-2xl border-2 cursor-pointer transition-all flex items-start gap-3', form.paymentMethod === 'online' ? 'border-rose-900 bg-rose-50/40 shadow-sm' : 'border-slate-200 bg-slate-50/50 hover:border-slate-300']">
              <input v-model="form.paymentMethod" type="radio" value="online" class="mt-1 accent-rose-900" />
              <div class="space-y-1">
                <span class="font-bold text-sm text-slate-900 font-serif block">অনলাইন পেমেন্ট (বিকাশ/নগদ)</span>
                <p class="text-xs text-slate-500">বিকাশ, নগদ, রকেট বা ডেবিট/ক্রেডিট কার্ডের মাধ্যমে পেমেন্ট করুন।</p>
              </div>
            </label>

          </div>
        </div>

      </div>

      <!-- Right: Order Summary Sidebar -->
      <div class="bg-white p-6 sm:p-8 rounded-3xl border border-slate-200/80 shadow-sm space-y-6 lg:col-span-1">
        <h3 class="text-lg font-bold font-serif text-slate-900 border-b border-slate-100 pb-3">আপনার অর্ডার (২ টি পণ্য)</h3>

        <!-- Items Preview -->
        <div class="space-y-3 max-h-56 overflow-y-auto">
          <div v-for="item in cartItems" :key="item.id" class="flex items-center gap-3 p-2 rounded-xl bg-slate-50 border border-slate-100">
            <img :src="item.image" class="w-12 h-12 rounded-lg object-cover shrink-0" alt="product" />
            <div class="flex-1 min-w-0">
              <h4 class="text-xs font-bold font-serif text-slate-900 truncate">{{ item.title }}</h4>
              <p class="text-[11px] text-slate-500">পরিমাণ: {{ item.qty }}</p>
            </div>
            <span class="text-xs font-extrabold text-rose-950">৳ {{ item.price }}</span>
          </div>
        </div>

        <!-- Totals Breakdown -->
        <div class="space-y-3 pt-4 border-t border-slate-100 text-xs sm:text-sm text-slate-600">
          <div class="flex justify-between">
            <span>সাবটোটাল</span>
            <span class="font-bold text-slate-900">৳ {{ subtotal }}</span>
          </div>
          <div class="flex justify-between">
            <span>ডেলিভারি চার্জ ({{ form.district }})</span>
            <span class="font-bold text-slate-900">৳ {{ deliveryFee }}</span>
          </div>
          <div class="flex justify-between items-center pt-3 border-t border-slate-100 text-base font-extrabold text-slate-900">
            <span>সর্বমোট প্রদেয়</span>
            <span class="text-rose-950 text-xl">৳ {{ finalTotal }}</span>
          </div>
        </div>

        <!-- Submit Button -->
        <div class="pt-2">
          <button 
            type="submit" 
            :disabled="isSubmitting" 
            class="w-full bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-4 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99] disabled:opacity-50 flex items-center justify-center gap-2"
          >
            <span v-if="isSubmitting" class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
            {{ isSubmitting ? 'প্রসেসিং হচ্ছে...' : 'অর্ডার কনফার্ম করুন 🎯' }}
          </button>
        </div>

        <!-- Trust Badges -->
        <div class="text-center pt-2 border-t border-slate-100 text-[11px] text-slate-400">
          🔒 আপনার তথ্য সম্পূর্ণ নিরাপদ ও সুরক্ষিত
        </div>

      </div>

    </form>

  </div>
</template>