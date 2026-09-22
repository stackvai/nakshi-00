<!-- pages/login.vue -->
<script setup lang="ts">
import { ref } from 'vue'

useHead({
  title: 'লগইন বা রেজিস্টার — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'আপনার অ্যাকাউন্টে লগইন করুন অথবা নতুন অ্যাকাউন্ট তৈরি করুন।' }
  ]
})

// Mode toggle: 'login' or 'register'
const authMode = ref<'login' | 'register'>('login')

// Form states
const loginForm = ref({
  emailOrPhone: '',
  password: '',
  rememberMe: false
})

const registerForm = ref({
  name: '',
  emailOrPhone: '',
  password: '',
  confirmPassword: ''
})

const showPassword = ref(false)
const isLoading = ref(false)
const successMessage = ref('')

const handleLogin = () => {
  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
    successMessage.value = 'সফলভাবে লগইন করা হয়েছে! হোম পেজে রিডাইরেক্ট করা হচ্ছে...'
    setTimeout(() => {
      navigateTo('/')
    }, 1500)
  }, 1000)
}

const handleRegister = () => {
  if (registerForm.value.password !== registerForm.value.confirmPassword) {
    alert('পাসওয়ার্ড মিলছে না!');
    return
  }
  isLoading.value = true
  setTimeout(() => {
    isLoading.value = false
    successMessage.value = 'অ্যাকাউন্ট সফলভাবে তৈরি হয়েছে! এবার লগইন করুন।'
    authMode.value = 'login'
    registerForm.value = { name: '', emailOrPhone: '', password: '', confirmPassword: '' }
    setTimeout(() => { successMessage.value = '' }, 4000)
  }, 1000)
}
</script>

<template>
  <div class="max-w-md mx-auto px-4 py-16 sm:py-24">

    <!-- Auth Card Container -->
    <div class="bg-white/90 backdrop-blur-2xl p-8 sm:p-10 rounded-3xl border border-slate-200/80 shadow-2xl shadow-rose-950/5 space-y-8 relative overflow-hidden">
      
      <!-- Decorative Gradient Glow -->
      <div class="absolute top-0 right-0 w-32 h-32 bg-gradient-to-br from-rose-500/10 to-amber-500/10 rounded-bl-full pointer-events-none"></div>

      <!-- Header & Mode Switcher Tabs -->
      <div class="text-center space-y-3">
        <span class="inline-block bg-rose-50 text-rose-900 border border-rose-100 text-xs font-bold px-3 py-1 rounded-full uppercase tracking-widest">
          নকশী কাঁথা স্টুডিও
        </span>
        <h1 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">
          {{ authMode === 'login' ? 'স্বাগতম ফিরে আসায়!' : 'নতুন অ্যাকাউন্ট তৈরি করুন' }}
        </h1>
        <p class="text-xs sm:text-sm text-slate-500">
          {{ authMode === 'login' ? 'আপনার অ্যাকাউন্টে প্রবেশ করতে তথ্য দিন।' : 'আপনার তথ্য দিয়ে দ্রুত রেজিস্ট্রেশন সম্পন্ন করুন।' }}
        </p>
      </div>

      <!-- Tab Switcher -->
      <div class="grid grid-cols-2 bg-slate-100 p-1.5 rounded-2xl border border-slate-200/60">
        <button 
          @click="authMode = 'login'; successMessage = ''"
          :class="['py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', authMode === 'login' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-500 hover:text-slate-800']"
        >
          লগইন
        </button>
        <button 
          @click="authMode = 'register'; successMessage = ''"
          :class="['py-2.5 rounded-xl font-bold text-xs sm:text-sm transition-all', authMode === 'register' ? 'bg-white text-rose-900 shadow-sm' : 'text-slate-500 hover:text-slate-800']"
        >
          রেজিস্ট্রেশন
        </button>
      </div>

      <!-- Success Alert -->
      <div v-if="successMessage" class="p-4 bg-emerald-50 border border-emerald-200 text-emerald-800 text-xs rounded-2xl text-center font-medium shadow-sm">
        {{ successMessage }}
      </div>

      <!-- 1. LOGIN FORM -->
      <form v-if="authMode === 'login'" @submit.prevent="handleLogin" class="space-y-5">
        <div class="space-y-1.5">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">ইমেইল বা মোবাইল নম্বর *</label>
          <input 
            v-model="loginForm.emailOrPhone" 
            type="text" 
            required 
            placeholder="example@gmail.com বা 01XXXXXXXXX" 
            class="w-full px-4.5 py-3.5 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
          />
        </div>

        <div class="space-y-1.5">
          <div class="flex justify-between items-center">
            <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">পাসওয়ার্ড *</label>
            <a href="#" class="text-xs text-rose-900 font-bold hover:underline">পাসওয়ার্ড ভুলে গেছেন?</a>
          </div>
          <div class="relative">
            <input 
              v-model="loginForm.password" 
              :type="showPassword ? 'text' : 'password'" 
              required 
              placeholder="••••••••" 
              class="w-full px-4.5 py-3.5 pr-12 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
            />
            <button type="button" @click="showPassword = !showPassword" class="absolute right-4 top-3.5 text-slate-400 hover:text-slate-600 text-xs font-bold">
              {{ showPassword ? 'লুকান' : 'দেখুন' }}
            </button>
          </div>
        </div>

        <div class="flex items-center gap-2">
          <input v-model="loginForm.rememberMe" type="checkbox" id="remember" class="w-4 h-4 accent-rose-900 rounded cursor-pointer" />
          <label for="remember" class="text-xs text-slate-600 cursor-pointer">আমাকে মনে রাখুন</label>
        </div>

        <button 
          type="submit" 
          :disabled="isLoading" 
          class="w-full bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-4 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99] disabled:opacity-50 flex items-center justify-center gap-2"
        >
          <span v-if="isLoading" class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
          {{ isLoading ? 'লগইন হচ্ছে...' : 'লগইন করুন 🚀' }}
        </button>
      </form>

      <!-- 2. REGISTER FORM -->
      <form v-else @submit.prevent="handleRegister" class="space-y-4">
        <div class="space-y-1">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">আপনার পূর্ণ নাম *</label>
          <input 
            v-model="registerForm.name" 
            type="text" 
            required 
            placeholder="আপনার নাম লিখুন" 
            class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
          />
        </div>

        <div class="space-y-1">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">ইমেইল বা মোবাইল নম্বর *</label>
          <input 
            v-model="registerForm.emailOrPhone" 
            type="text" 
            required 
            placeholder="example@gmail.com বা 01XXXXXXXXX" 
            class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
          />
        </div>

        <div class="space-y-1">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">পাসওয়ার্ড *</label>
          <input 
            v-model="registerForm.password" 
            type="password" 
            required 
            placeholder="কমপক্ষে ৬ ডিজিটের পাসওয়ার্ড" 
            class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
          />
        </div>

        <div class="space-y-1">
          <label class="text-xs font-bold text-slate-700 tracking-wide uppercase">পাসওয়ার্ড নিশ্চিত করুন *</label>
          <input 
            v-model="registerForm.confirmPassword" 
            type="password" 
            required 
            placeholder="পুনরায় পাসওয়ার্ড লিখুন" 
            class="w-full px-4.5 py-3 rounded-2xl bg-slate-50 border border-slate-200 text-sm focus:outline-none focus:border-rose-900 focus:bg-white transition-all shadow-inner"
          />
        </div>

        <button 
          type="submit" 
          :disabled="isLoading" 
          class="w-full bg-gradient-to-r from-rose-900 to-rose-950 hover:from-rose-950 hover:to-slate-950 text-white font-bold py-3.5 rounded-2xl text-sm transition-all shadow-xl shadow-rose-950/20 active:scale-[0.99] disabled:opacity-50 flex items-center justify-center gap-2 mt-2"
        >
          <span v-if="isLoading" class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin"></span>
          {{ isLoading ? 'তৈরি হচ্ছে...' : 'রেজিস্ট্রেশন সম্পন্ন করুন 🎯' }}
        </button>
      </form>

      <!-- Social Login Divider -->
      <div class="relative flex py-2 items-center">
        <div class="flex-grow border-t border-slate-200"></div>
        <span class="flex-shrink mx-4 text-xs text-slate-400 uppercase tracking-widest">অথবা</span>
        <div class="flex-grow border-t border-slate-200"></div>
      </div>

      <!-- Social Buttons -->
      <div class="grid grid-cols-2 gap-3">
        <button type="button" class="flex items-center justify-center gap-2 py-3 px-4 rounded-2xl border border-slate-200 bg-slate-50 hover:bg-slate-100 text-xs font-bold text-slate-700 transition-colors shadow-sm">
          🌐 গুগল লগইন
        </button>
        <button type="button" class="flex items-center justify-center gap-2 py-3 px-4 rounded-2xl border border-slate-200 bg-slate-50 hover:bg-slate-100 text-xs font-bold text-slate-700 transition-colors shadow-sm">
          📘 ফেসবুক লগইন
        </button>
      </div>

    </div>

  </div>
</template>