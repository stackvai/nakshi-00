<!-- pages/forgot-password.vue -->
<script setup lang="ts">
import { ref, onUnmounted } from 'vue'

useHead({
  title: 'পাসওয়ার্ড পুনরুদ্ধার — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'জিমেইলে ওটিপি কোড পাঠিয়ে আপনার পাসওয়ার্ড নিরাপদে পরিবর্তন করুন।' }
  ]
})

// Wizard Steps: 1 = Enter Email, 2 = Verify OTP & Set New Password
const currentStep = ref<1 | 2>(1)

const emailInput = ref('')
const otpCode = ref(['', '', '', ''])
const newPassword = ref('')
const confirmNewPassword = ref('')
const showNewPassword = ref(false)
const showConfirmPassword = ref(false)

const isLoading = ref(false)
const errorMessage = ref('')
const successMessage = ref('')

// Resend Timer (60 seconds)
const resendTimer = ref(60)
let timerInterval: any = null

const startResendTimer = () => {
  resendTimer.value = 60
  clearInterval(timerInterval)
  timerInterval = setInterval(() => {
    if (resendTimer.value > 0) {
      resendTimer.value--
    } else {
      clearInterval(timerInterval)
    }
  }, 1000)
}

onUnmounted(() => {
  clearInterval(timerInterval)
})

// STEP 1: Send Reset OTP to Gmail
const handleSendResetOtp = () => {
  errorMessage.value = ''
  if (!emailInput.value || !emailInput.value.includes('@')) {
    errorMessage.value = 'সঠিক জিমেইল বা ইমেইল ঠিকানা লিখুন।'
    return
  }

  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
    currentStep.value = 2
    successMessage.value = `আপনার ${emailInput.value} ঠিকানায় পাসওয়ার্ড রিকভারি কোড পাঠানো হয়েছে।`
    startResendTimer()
  }, 1000)
}

// STEP 2: Verify OTP & Reset Password
const handleResetPassword = () => {
  errorMessage.value = ''
  const enteredOtp = otpCode.value.join('')

  if (enteredOtp.length < 4) {
    errorMessage.value = 'সম্পূর্ণ ৪ ডিজিটের কোডটি লিখুন।'
    return
  }

  if (newPassword.value.length < 6) {
    errorMessage.value = 'নতুন পাসওয়ার্ড কমপক্ষে ৬ ডিজিটের হতে হবে।'
    return
  }

  if (newPassword.value !== confirmNewPassword.value) {
    errorMessage.value = 'পাসওয়ার্ড দুটি মিলছে না!'
    return
  }

  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
    successMessage.value = 'পাসওয়ার্ড সফলভাবে পরিবর্তন হয়েছে! লগইন পেজে রিডাইরেক্ট করা হচ্ছে...'
    setTimeout(() => {
      navigateTo('/login')
    }, 1800)
  }, 1200)
}
</script>

<template>
  <div class="max-w-md mx-auto px-4 py-16 sm:py-24">

    <!-- Card Container -->
    <div class="bg-white/90 backdrop-blur-2xl p-8 sm:p-10 rounded-3xl border border-slate-200/80 shadow-2xl shadow-rose-950/5 space-y-8 relative overflow-hidden">
      
      <!-- Ambient Glow -->
      <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-amber-500/10 to-rose-500/10 rounded-bl-full pointer-events-none"></div>

      <!-- Header -->
      <div class="text-center space-y-3">
        <span class="inline-block bg-rose-50 text-rose-900 border border-rose-100 text-xs font-bold px-3.5 py-1 rounded-full uppercase tracking-widest">
          পাসওয়ার্ড রিকভারি
        </span>
        <h1 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">
          {{ currentStep === 1 ? 'পাসওয়ার্ড ভুলে গেছেন?' : 'নতুন পাসওয়ার্ড সেট করুন' }}
        </h1>
        <p class="text-xs sm:text-sm text-slate-500">
          {{ currentStep === 1 ? 'আপনার নিবন্ধিত জিমেইল ঠিকানা দিয়ে কোড পাঠান।' : 'ওটিপি কোড যাচাই করে নতুন পাসওয়ার্ড দিন।' }}
        </p>
      </div>

      <!-- Alerts -->
      <div v-if="errorMessage" class="p-4 bg-rose-50 border border-rose-200 text-rose-800 text-xs rounded-2xl text-center font-medium shadow-sm">
        ⚠️ {{ errorMessage }}
      </div>

      <div v-if="successMessage" class="p-4 bg-emerald-50 border border-emerald-200 text-emerald-800 text-xs rounded-2xl text-center font-medium shadow-sm">
        🎉 {{ successMessage }}
      </div>

      <!-- ================= STEP 1: ENTER EMAIL FOR RESET ================= -->
      <form v-if="currentStep === 1" @submit.prevent="handleSendResetOtp" class="space-y-5">
        <div class="space-y-1.5">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">জিমেইল বা ইমেইল ঠিকানা *</label>
          <input 
            v-model="emailInput" 
            type="email" 
            required 
            placeholder="yourname@gmail.com" 
            class="w-full px-4.5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
          />
        </div>

        <button 
          type="submit" 
          :disabled="isLoading" 
          class="w-full bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-4 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99] disabled:opacity-50 flex items-center justify-center gap-2"
        >
          <span v-if="isLoading" class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
          {{ isLoading ? 'কোড পাঠানো হচ্ছে...' : 'পাসওয়ার্ড রিসেট কোড পাঠান 📨' }}
        </button>
      </form>


      <!-- ================= STEP 2: VERIFY OTP & SET NEW PASSWORD ================= -->
      <form v-else @submit.prevent="handleResetPassword" class="space-y-4">
        
        <!-- OTP Input boxes -->
        <div class="space-y-2">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase block text-center">৪ ডিজিটের ওটিপি (OTP) কোড দিন</label>
          <div class="flex justify-center gap-3">
            <input 
              v-for="(digit, index) in otpCode" 
              :key="index"
              v-model="otpCode[index]"
              type="text" 
              maxlength="1" 
              class="w-12 h-12 text-center text-lg font-bold rounded-xl bg-slate-50 border border-slate-200 focus:border-rose-900 focus:bg-white focus:outline-none shadow-inner"
            />
          </div>
          <div class="text-center pt-1">
            <span v-if="resendTimer > 0" class="text-xs text-slate-400">কোড পাননি? পুনরায় পাঠাতে অপেক্ষা করুন {{ resendTimer }} সেকেন্ড</span>
            <button v-else type="button" @click="startResendTimer" class="text-xs text-rose-900 font-bold hover:underline">কোড পুনরায় পাঠান</button>
          </div>
        </div>

        <div class="space-y-1 pt-2">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">নতুন পাসওয়ার্ড *</label>
          <div class="relative">
            <input 
              v-model="newPassword" 
              :type="showNewPassword ? 'text' : 'password'" 
              required 
              placeholder="কমপক্ষে ৬ ডিজিটের পাসওয়ার্ড" 
              class="w-full px-4.5 py-3 pr-12 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
            />
            <button type="button" @click="showNewPassword = !showNewPassword" class="absolute right-4 top-3 text-slate-400 hover:text-slate-600 text-xs font-bold">
              {{ showNewPassword ? 'লুকান' : 'দেখুন' }}
            </button>
          </div>
        </div>

        <div class="space-y-1">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">নতুন পাসওয়ার্ড নিশ্চিত করুন *</label>
          <div class="relative">
            <input 
              v-model="confirmNewPassword" 
              :type="showConfirmPassword ? 'text' : 'password'" 
              required 
              placeholder="পুনরায় পাসওয়ার্ড লিখুন" 
              class="w-full px-4.5 py-3 pr-12 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
            />
            <button type="button" @click="showConfirmPassword = !showConfirmPassword" class="absolute right-4 top-3 text-slate-400 hover:text-slate-600 text-xs font-bold">
              {{ showConfirmPassword ? 'লুকান' : 'দেখুন' }}
            </button>
          </div>
        </div>

        <div class="flex gap-3 pt-2">
          <button 
            type="button" 
            @click="currentStep = 1; successMessage = ''" 
            class="px-4 py-3.5 rounded-2xl border border-slate-200 bg-slate-100 text-slate-700 text-xs font-bold hover:bg-slate-200 transition-colors"
          >
            ← ইমেইল বদলান
          </button>
          
          <button 
            type="submit" 
            :disabled="isLoading" 
            class="flex-1 bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-3.5 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99] disabled:opacity-50 flex items-center justify-center gap-2"
          >
            <span v-if="isLoading" class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
            {{ isLoading ? 'পরিবর্তন হচ্ছে...' : 'পাসওয়ার্ড পরিবর্তন করুন 🔒' }}
          </button>
        </div>

      </form>

      <!-- Footer login link -->
      <div class="text-center pt-2 border-t border-slate-100">
        <p class="text-xs text-slate-500">
          পাসওয়ার্ড মনে আছে? 
          <NuxtLink to="/login" class="text-rose-900 font-bold hover:underline ml-1">লগইন করুন</NuxtLink>
        </p>
      </div>

    </div>

  </div>
</template>