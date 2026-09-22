<!-- components/layout/Footer.vue -->
<template>
  <footer class="bg-slate-900 text-slate-300 pt-12 pb-6 border-t border-slate-800">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 mb-12">
      
      <!-- Brand & Story -->
      <div>
        <div class="flex items-center gap-2 mb-4">
          <div class="w-8 h-8 rounded-full bg-rose-800 flex items-center justify-center text-white font-bold text-base">
            ন
          </div>
          <span class="text-xl font-bold text-white font-serif">নকশী কাঁথা</span>
        </div>
        <p class="text-xs sm:text-sm text-slate-400 leading-relaxed mb-4">
          আমরা গ্রামীণ কারিগরদের ঐতিহ্যবাহী নকশী কাঁথার শিল্পকে সরাসরি আপনাদের কাছে পৌঁছে দিচ্ছি। ১০০% হাতে তৈরি খাঁটি সুতির মানসম্মত পণ্য।
        </p>
      </div>

      <!-- Quick Links -->
      <div>
        <h4 class="text-white text-base font-semibold mb-4 border-b border-rose-900/60 pb-2 inline-block">
          গুরুত্বপূর্ণ লিংক
        </h4>
        <ul class="space-y-2 text-sm">
          <li><NuxtLink to="/about" class="hover:text-amber-400 transition-colors">আমাদের সম্পর্কে</NuxtLink></li>
          <li><NuxtLink to="/products" class="hover:text-amber-400 transition-colors">সকল প্রোডাক্ট</NuxtLink></li>
          <li><NuxtLink to="/blog" class="hover:text-amber-400 transition-colors">নকশী কাঁথার ইতিহাস</NuxtLink></li>
          <li><NuxtLink to="/contact" class="hover:text-amber-400 transition-colors">যোগাযোগ</NuxtLink></li>
        </ul>
      </div>

      <!-- Help & Policies -->
      <div>
        <h4 class="text-white text-base font-semibold mb-4 border-b border-rose-900/60 pb-2 inline-block">
          কাস্টমার সেবামূল নীতি
        </h4>
        <ul class="space-y-2 text-sm">
          <li><NuxtLink to="/privacy-policy" class="hover:text-amber-400 transition-colors">প্রাইভেসি পলিসি</NuxtLink></li>
          <li><NuxtLink to="/terms" class="hover:text-amber-400 transition-colors">টার্মস ও কন্ডিশন</NuxtLink></li>
          <li><NuxtLink to="/return-policy" class="hover:text-amber-400 transition-colors">রিটার্ন ও রিফান্ড নীতি</NuxtLink></li>
          <li><NuxtLink to="/faq" class="hover:text-amber-400 transition-colors">সাধারণ জিজ্ঞাসাবলী (FAQ)</NuxtLink></li>
        </ul>
      </div>

      <!-- Contact Info -->
      <div>
        <h4 class="text-white text-base font-semibold mb-4 border-b border-rose-900/60 pb-2 inline-block">
          যোগাযোগ করুন
        </h4>
        <ul class="space-y-2 text-sm text-slate-400">
          <li class="flex items-center gap-2">📍 ঢাকা, বাংলাদেশ</li>
          <li class="flex items-center gap-2">📞 +৮৮০ ১৭০০-০০০০০</li>
          <li class="flex items-center gap-2">✉️ support@nakshikatha.com</li>
        </ul>
      </div>

    </div>

    <!-- Copyright & Bottom Bar -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 pt-6 border-t border-slate-800 flex flex-col sm:flex-row justify-between items-center text-xs text-slate-500 gap-4">
      <p>© {{ new Date().getFullYear() }} নকশী কাঁথা। সর্বস্বত্ব সংরক্ষিত।</p>
      <div class="flex items-center gap-4">
        <span>নিরাপদ পেমেন্ট: বিকাশ / নগদ / ক্যাশ অন ডেলিভারি</span>
      </div>
    </div>
  </footer>
</template>