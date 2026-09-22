<!-- pages/about.vue -->
<script setup lang="ts">
useHead({
  title: 'আমাদের গল্প ও ঐতিহ্য — নকশী কাঁথা স্টুডিও',
  meta: [
    { name: 'description', content: 'জামালপুরের শতবর্ষী লোকশিল্প, সুতোর ফোঁড়ে বোনা নারীর গল্প এবং আমাদের ঐতিহ্যবাহী পথচলার ইতিহাস।' }
  ]
})
</script>

<template>
  <div class="max-w-7xl mx-auto px-4 space-y-24 lg:space-y-36 py-12">

    <!-- 1. Cinematic Hero Storytelling Section -->
    <section class="text-center max-w-4xl mx-auto space-y-6">
      <span class="inline-block bg-amber-100 text-amber-900 border border-amber-200 text-xs font-bold px-3.5 py-1.5 rounded-full uppercase tracking-widest">
        আমাদের শেকড় ও ঐতিহ্য
      </span>
      <h1 class="text-3xl sm:text-5xl lg:text-6xl font-extrabold font-serif text-slate-900 leading-tight">
        সুতো আর ফোঁড়ের ক্যানভাসে আবহমান বাংলার জীবন্ত ইতিহাস
      </h1>
      <p class="text-slate-600 text-base sm:text-lg leading-relaxed max-w-3xl mx-auto">
        পৌষের শীতের সকালে লেপের ওম, কিংবা দাদি-নানিদের কুঁড়েঘরের বারান্দায় রূপকথার গল্প শোনার সোনালী দিনগুলো কি মনে পড়ে? নকশী কাঁথা কেবল একটি কাপড় নয়—এটি গ্রামীণ নারীর অব্যক্ত আবেগ, শিল্পবোধ এবং প্রজন্ম থেকে প্রজন্মে বয়ে চলা এক পৈত্রিক উত্তরাধিকার।
      </p>
    </section>

    <!-- 2. The Genesis Story: Where It All Began -->
    <section class="grid lg:grid-cols-2 gap-12 lg:gap-16 items-center">
      <div class="space-y-6">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">আমাদের শুরুর গল্প</span>
        <h2 class="text-2xl sm:text-4xl font-bold font-serif text-slate-900 leading-snug">
          জামালপুরের মাটির গন্ধ থেকে শহুরে আঙিনায়
        </h2>
        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
          আমাদের পথচলা শুরু হয়েছিল ময়মনসিংহ অঞ্চলের ঐতিহ্যবাহী জনপদ জামালপুর থেকে। যেখানে ব্রহ্মপুত্র নদের ঢেউয়ের মতো এপার-ওপার ছড়িয়ে আছে গ্রামীণ নারীদের হাতের জাদুকরী নিখুঁত ফোঁড়। যান্ত্রিকতার এই যুগে যখন সবকিছুই প্রিন্ট বা মেশিনের ছাঁচে তৈরি, তখন আমরা চেয়েছিলাম শেকড়ের সেই আসল রূপটিকে বাঁচিয়ে রাখতে।
        </p>
        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
          আজ **নকশী কাঁথা স্টুডিও** কোনো সাধারণ ই-কমার্স ব্র্যান্ড নয়; এটি শত শত গ্রামীণ নারীর মেধার মূল্যায়ন এবং জামালপুরের জিআই (GI) সনদপ্রাপ্ত হস্তশিল্পকে বিশ্ব দরবারে পৌঁছে দেওয়ার এক নিরলস আন্দোলন।
        </p>
      </div>
      <div class="grid grid-cols-2 gap-4">
        <div class="aspect-[3/4] rounded-2xl overflow-hidden shadow-lg">
          <img src="https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600" class="w-full h-full object-cover hover:scale-105 transition-transform duration-500" alt="Traditional Katha" />
        </div>
        <div class="aspect-[3/4] rounded-2xl overflow-hidden shadow-lg mt-10">
          <img src="https://images.unsplash.com/photo-1600121848594-d8644e57abab?q=80&w=600" class="w-full h-full object-cover hover:scale-105 transition-transform duration-500" alt="Detailed stitches" />
        </div>
      </div>
    </section>

    <!-- 3. Sensory Narrative: The Journey of a Single Kantha -->
    <section class="bg-rose-950 text-white rounded-3xl p-8 sm:p-16 relative overflow-hidden space-y-12">
      <div class="absolute inset-0 opacity-10 bg-[radial-gradient(#d97706_1px,transparent_1px)] [background-size:16px_16px]"></div>
      
      <div class="text-center max-w-2xl mx-auto space-y-3 relative z-10">
        <span class="text-xs font-bold text-amber-300 uppercase tracking-widest">রূপকথার মতো বুনন</span>
        <h2 class="text-2xl sm:text-4xl font-bold font-serif">একটি কাঁথা তৈরিতে লাগে শত ঘণ্টার সাধনা</h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8 relative z-10">
        <div class="bg-white/5 border border-white/10 p-6 sm:p-8 rounded-2xl space-y-4">
          <div class="w-12 h-12 rounded-xl bg-amber-500/20 text-amber-300 flex items-center justify-center font-bold text-xl">০১</div>
          <h3 class="text-lg font-bold font-serif">প্রি-ওয়াশড সুতির নির্বাচন</h3>
          <p class="text-rose-100/80 text-xs sm:text-sm leading-relaxed">
            সরাসরি কারখানা থেকে আনা হয় না। শতভাগ প্রি-ওয়াশড নরম সুতি কাপড় বাছা হয়, যা ধোয়ার পরেও সুতার শক্তি ও কোমলতা বজায় রাখে।
          </p>
        </div>
        <div class="bg-white/5 border border-white/10 p-6 sm:p-8 rounded-2xl space-y-4">
          <div class="w-12 h-12 rounded-xl bg-amber-500/20 text-amber-300 flex items-center justify-center font-bold text-xl">০২</div>
          <h3 class="text-lg font-bold font-serif">মুক্তহাতে নকশা অঙ্কন</h3>
          <p class="text-rose-100/80 text-xs sm:text-sm leading-relaxed">
            কোনো আধুনিক প্রিন্টার নয়। শিল্পীদের হাতের ছোঁয়ায় কদম ফুল, ময়ূরপঙ্খী নৌকা, লতা-পাতা ও পল্লিপ্রকৃতির গল্প ফুটে ওঠে কাপড়ের জমিনে।
          </p>
        </div>
        <div class="bg-white/5 border border-white/10 p-6 sm:p-8 rounded-2xl space-y-4">
          <div class="w-12 h-12 rounded-xl bg-amber-500/20 text-amber-300 flex items-center justify-center font-bold text-xl">০৩</div>
          <h3 class="text-lg font-bold font-serif">নিখুঁত ফোঁড়ের জাদু</h3>
          <p class="text-rose-100/80 text-xs sm:text-sm leading-relaxed">
            প্রতিটি সূচ ও সুতোর টানে লুকিয়ে থাকে শিল্পীর আবেগ। দিনের পর দিন সুনিপুণ ফোঁড়ে গড়ে ওঠে প্রজন্ম থেকে প্রজন্মে ব্যবহারের উপযোগী মাস্টারপিস।
          </p>
        </div>
      </div>
    </section>

    <!-- 4. Artisan Empowerment & Impact Statistics -->
    <section class="space-y-12">
      <div class="text-center max-w-2xl mx-auto space-y-3">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">সামাজিক প্রভাব</span>
        <h2 class="text-2xl sm:text-4xl font-bold font-serif text-slate-900">যেখানে প্রতিটি ক্রয়ে বদলায় একেকটি জীবন</h2>
        <p class="text-sm text-slate-600">আমাদের সাথে যুক্ত আছেন জামালপুরের মেলান্দহ, মাদারগঞ্জ ও ইসলামপুর উপজেলার প্রান্তিক নারী কারিগররা।</p>
      </div>

      <div class="grid grid-cols-2 lg:grid-cols-4 gap-6">
        <div class="p-8 bg-slate-50 rounded-2xl border border-slate-200/60 text-center space-y-2">
          <h3 class="text-3xl sm:text-4xl font-bold font-serif text-rose-900">৬০০+</h3>
          <p class="text-xs sm:text-sm text-slate-600 font-medium">স্বাবলম্বী নারী কারিগর</p>
        </div>
        <div class="p-8 bg-slate-50 rounded-2xl border border-slate-200/60 text-center space-y-2">
          <h3 class="text-3xl sm:text-4xl font-bold font-serif text-rose-900">১৫,০০০+</h3>
          <p class="text-xs sm:text-sm text-slate-600 font-medium">সন্তুষ্ট পরিবার ও ক্রেতা</p>
        </div>
        <div class="p-8 bg-slate-50 rounded-2xl border border-slate-200/60 text-center space-y-2">
          <h3 class="text-3xl sm:text-4xl font-bold font-serif text-rose-900">১০০%</h3>
          <p class="text-xs sm:text-sm text-slate-600 font-medium">হস্তশিল্পের নিশ্চয়তা</p>
        </div>
        <div class="p-8 bg-slate-50 rounded-2xl border border-slate-200/60 text-center space-y-2">
          <h3 class="text-3xl sm:text-4xl font-bold font-serif text-rose-900">জিআই</h3>
          <p class="text-xs sm:text-sm text-slate-600 font-medium">সনদপ্রাপ্ত অরিজিনাল পণ্য</p>
        </div>
      </div>
    </section>

    <!-- 5. Cultural Significance: Why Nakshi Katha Matters -->
    <section class="grid lg:grid-cols-2 gap-12 items-center bg-slate-50 p-8 sm:p-14 rounded-3xl border border-slate-200/60">
      <div class="space-y-6">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">ঐতিহাসিক গুরুত্ব</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">
          একটি কাঁথার ভেতর লুকিয়ে থাকে একটি পুরো পরিবারের গল্প
        </h2>
        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
          প্রাচীনকালে গ্রামীণ নারীরা পুরনো শাড়ি ও সুতির কাপড় জোড়া লাগিয়ে কাঁথা তৈরি করতেন। শীতের রাতের উষ্ণতার পাশাপাশি এতে ফুটিয়ে তোলা হতো তাদের মনের সুপ্ত আশা, স্বপ্ন আর পারিপার্শ্বিক প্রকৃতির রূপ।
        </p>
        <p class="text-slate-600 text-sm sm:text-base leading-relaxed">
          আজকের দিনে নকশী কাঁথা কেবল শীত নিবারণের মাধ্যম নয়; এটি আমাদের ঘরের ড্রয়িং রুম কিংবা শোবার ঘরের সৌন্দর্য বহুগুণ বাড়িয়ে দেয় এবং বাঙালি আভিজাত্যের প্রতীক হয়ে উঠেছে।
        </p>
      </div>
      <div class="rounded-2xl overflow-hidden aspect-[4/3] shadow-md">
        <img src="https://images.unsplash.com/photo-1616627547584-bf28cee262db?q=80&w=800" class="w-full h-full object-cover" alt="Cultural Katha" />
      </div>
    </section>

    <!-- 6. The GI Certification Story -->
    <section class="bg-amber-50 border border-amber-200 rounded-3xl p-8 sm:p-12 flex flex-col md:flex-row items-center gap-8">
      <div class="w-20 h-20 rounded-2xl bg-amber-500 text-slate-950 font-bold flex items-center justify-center text-2xl shrink-0 font-serif shadow-sm">
        জিআই
      </div>
      <div class="space-y-3">
        <span class="text-xs font-bold text-amber-800 uppercase tracking-wider">ভৌগোলিক নির্দেশক স্বীকৃতি</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">জামালপুরের নকশী কাঁথার জিআই (GI) সনদ</h2>
        <p class="text-sm text-slate-700 leading-relaxed">
          বাংলাদেশের হস্তশিল্পের ইতিহাসে জামালপুরের নকশী কাঁথা একটি অনন্য মাইলফলক স্পর্শ করেছে। ভৌগোলিক নির্দেশক (GI) পণ্য হিসেবে স্বীকৃতির মাধ্যমে আজ বিশ্বদরবারে জামালপুরের এই লোকশিল্প তার আসল মর্যাদা ও স্বতন্ত্র ভৌগোলিক পরিচয় লাভ করেছে। আমরা গর্বের সাথে সেই আসল ঐতিহ্যটি আপনার দোরগোড়ায় পৌঁছে দিচ্ছি।
        </p>
      </div>
    </section>

    <!-- 7. Artisan Stories & Personal Voices -->
    <section class="space-y-10">
      <div class="text-center max-w-2xl mx-auto space-y-3">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">শিল্পীর মুখ থেকে</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">যাঁদের হাতের জাদুতে জীবন্ত হয় কাঁথা</h2>
        <p class="text-sm text-slate-600">মেলান্দহের হস্তশিল্পী রেহানা বেগমের জীবনের গল্প।</p>
      </div>
      <div class="bg-white border border-slate-200/80 p-8 sm:p-12 rounded-3xl shadow-sm grid lg:grid-cols-3 gap-8 items-center">
        <div class="aspect-square rounded-2xl overflow-hidden shadow-sm">
          <img src="https://images.unsplash.com/photo-1584100936595-c0654b55a2e2?q=80&w=600" class="w-full h-full object-cover" alt="Artisan Rehana" />
        </div>
        <div class="lg:col-span-2 space-y-4">
          <div class="flex text-amber-400 text-sm">★★★★★</div>
          <p class="text-slate-700 text-sm sm:text-base italic leading-relaxed">
            "আগে নিজের পরিবারের জন্যই শুধু কাঁথা সেলাই করতাম। এখন নকশী কাঁথা স্টুডিওর মাধ্যমে আমার হাতের তৈরি কাজ দেশের গণ্ডি পেরিয়ে ঢাকা, চট্টগ্রাম এমনকি প্রবাসীদের ঘরেও পৌঁছে যায়। এই কাজের উপার্জনেই আমি আমার মেয়ের পড়াশোনার খরচ চালাই। নিজের কাজ নিয়ে আজ আমার ভীষণ গর্ব হয়।"
          </p>
          <div>
            <h4 class="font-bold text-slate-900 text-base font-serif">রেহানা বেগম</h4>
            <p class="text-xs text-slate-500">মাস্টার কারিগর, জামালপুর</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 8. Our Quality Promise & Material Standards -->
    <section class="space-y-8">
      <div class="text-center max-w-2xl mx-auto space-y-3">
        <span class="text-xs font-bold text-rose-900 uppercase tracking-wider">গুণগত মান</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">যে কারণে আমাদের মান অনন্য</h2>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div class="p-6 bg-white rounded-2xl border border-slate-200/60 shadow-sm space-y-3">
          <div class="w-10 h-10 rounded-xl bg-rose-50 text-rose-900 font-bold flex items-center justify-center text-lg">🌿</div>
        <h3 class="font-bold text-lg font-serif text-slate-900">১০০% খাঁটি সুতি</h3>
          <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">কোনো কৃত্রিম পলিয়েস্টার মিশ্রণ নয়, সম্পূর্ণ আরামদায়ক ও প্রাকৃতিক সুতি কাপড় দিয়ে তৈরি।</p>
        </div>
        <div class="p-6 bg-white rounded-2xl border border-slate-200/60 shadow-sm space-y-3">
          <div class="w-10 h-10 rounded-xl bg-amber-50 text-amber-900 font-bold flex items-center justify-center text-lg">🎨</div>
          <h3 class="font-bold text-lg font-serif text-slate-900">পাকা ও নিরাপদ রং</h3>
          <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">বারবার ধোয়ার পরেও কাপড়ের রং ফ্যাকাশে হয় না, থাকে একেবারে নতুনের মতো উজ্জ্বল।</p>
        </div>
        <div class="p-6 bg-white rounded-2xl border border-slate-200/60 shadow-sm space-y-3">
          <div class="w-10 h-10 rounded-xl bg-emerald-50 text-emerald-900 font-bold flex items-center justify-center text-lg">🔒</div>
          <h3 class="font-bold text-lg font-serif text-slate-900">ক্যাশ অন ডেলিভারি চেক</h3>
          <p class="text-xs sm:text-sm text-slate-600 leading-relaxed">পণ্য হাতে পেয়ে ভালো করে যাচাই করে তারপর মূল্য পরিশোধের সম্পূর্ণ সুবিধা।</p>
        </div>
      </div>
    </section>

    <!-- 9. Sustainability and Eco-Friendly Crafting -->
    <section class="bg-emerald-950 text-white rounded-3xl p-8 sm:p-14 space-y-6">
      <div class="max-w-3xl space-y-4">
        <span class="inline-block bg-emerald-500/20 text-emerald-300 border border-emerald-400/30 text-xs px-3 py-1 rounded-full">পরিবেশবান্ধব প্রয়াস</span>
        <h2 class="text-2xl sm:text-4xl font-bold font-serif leading-snug">
          প্রকৃতির সাথে বন্ধুত্বের মেলবন্ধন
        </h2>
        <p class="text-emerald-100/90 text-sm sm:text-base leading-relaxed">
          আমাদের পুরো উৎপাদন প্রক্রিয়ায় পরিবেশের সুরক্ষাকে সর্বোচ্চ প্রাধান্য দেওয়া হয়। ক্ষতিকর কেমিক্যাল বা সিন্থেটিক উপাদান বর্জন করে প্রাকৃতিক সুতা এবং পরিবেশবান্ধব রং ব্যবহার করা হয়, যা আপনার সংবেদনশীল ত্বক এবং শিশুর স্বাস্থ্যের জন্য সম্পূর্ণ নিরাপদ।
        </p>
      </div>
    </section>

    <!-- 10. Founder & Artisan Letter / Deep Story Section -->
    <section class="grid lg:grid-cols-2 gap-12 items-center bg-amber-50/60 p-8 sm:p-14 rounded-3xl border border-amber-200">
      <div class="rounded-2xl overflow-hidden aspect-[4/3] shadow-md">
        <img src="https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af?q=80&w=800" class="w-full h-full object-cover" alt="Artisan community" />
      </div>
      <div class="space-y-6">
        <span class="text-xs font-bold text-amber-800 uppercase tracking-wider">আমাদের প্রতিজ্ঞা</span>
        <h2 class="text-2xl sm:text-3xl font-bold font-serif text-slate-900">
          "আমরা শুধু ব্যবসা করি না, আমরা ইতিহাস সংরক্ষণ করি"
        </h2>
        <p class="text-slate-700 text-sm sm:text-base leading-relaxed">
          যখন একজন মা তার নবজাতক সন্তানের জন্য আমাদের বেবি কাঁথাটি হাতে নেন, কিংবা কোনো প্রবাসী বাঙালি বিদেশের মাটিতে বসে দেশের সুবাস ছড়াতে আমাদের বেডশীটটি ব্যবহার করেন—সেখানেই আমাদের সার্থকতা। 
        </p>
        <p class="text-slate-700 text-sm sm:text-base leading-relaxed">
          আমাদের লক্ষ্য প্রতিটি ঘরে আবহমান বাংলার ঐতিহ্যকে আধুনিক ও মার্জিত রূপে ফুটিয়ে তোলা। আপনার আস্থাই আমাদের কাজের সবচেয়ে বড় অনুপ্রেরণা।
        </p>
        <div class="pt-2">
          <NuxtLink to="/" class="inline-block bg-rose-900 hover:bg-rose-950 text-white font-bold px-7 py-3 rounded-xl text-sm transition-colors shadow-sm">
            আমাদের কালেকশন দেখুন 🛍️
          </NuxtLink>
        </div>
      </div>
    </section>

    <!-- 11. Final Call to Action Section -->
    <section class="text-center max-w-2xl mx-auto space-y-6 py-6">
      <h2 class="text-2xl sm:text-4xl font-bold font-serif text-slate-900">আপনার ঘরের জন্য বেছে নিন খাঁটি ঐতিহ্য</h2>
      <p class="text-sm sm:text-base text-slate-600">জামালপুরের শতবর্ষী হাতের কাজের ছোঁয়ায় আপনার ঘরকে করে তুলুন আরও উষ্ণ ও সুন্দর।</p>
      <div class="flex justify-center gap-4">
        <NuxtLink to="/" class="bg-rose-900 hover:bg-rose-950 text-white font-bold px-8 py-3.5 rounded-xl text-sm transition-colors shadow-md">
          সকল আইটেম 🏠
        </NuxtLink>
      </div>
    </section>

  </div>
</template>