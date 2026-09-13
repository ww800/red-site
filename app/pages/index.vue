<script setup lang="ts">
const isMenuOpen = ref(false)

const navigation = [
  { label: '首页', href: '/' },
  { label: '产品', href: '/products' },
  { label: '关于', href: '/about' },
  { label: '团队', href: '/team' },
  { label: '联系', href: '/contact' },
]

const categories = [
  { name: '服饰饰品', slug: 'fashion', icon: '织', description: '以传统纹样为灵感，重释日常穿戴与生活美学。' },
  { name: '花竹帽IP', slug: 'flower-bamboo-hat', icon: '帽', description: '从毛南族花竹帽出发，构建可持续的文化创意符号。' },
  { name: '文创衍生', slug: 'cultural-creative', icon: '韵', description: '让非遗工艺进入更多场景，成为可亲近的当代礼物。' },
]

const highlights = [
  { icon: '01', title: '跨学科团队', description: '文化、设计与商业协同共创' },
  { icon: '02', title: '聚焦东盟', description: '连接区域市场与文化共鸣' },
  { icon: '03', title: '三阶段闭环', description: '研发、运营、出海持续迭代' },
]

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<template>
  <div class="min-h-screen overflow-hidden bg-[#f8f1e5] text-[#35271d]">
    <header class="relative z-20 border-b border-[#b58b54]/25 bg-[#f8f1e5]/95 backdrop-blur">
      <div class="mx-auto flex max-w-7xl items-center justify-between px-6 py-5 lg:px-10">
        <NuxtLink to="/" class="font-serif text-lg font-bold tracking-[0.12em] text-[#4a2f20]" @click="closeMenu">织锦传韵·美物焕新</NuxtLink>
        <nav class="hidden items-center gap-8 text-sm text-[#715744] md:flex" aria-label="主导航">
          <NuxtLink v-for="item in navigation" :key="item.href" :to="item.href" class="transition-colors hover:text-[#9a632c]">{{ item.label }}</NuxtLink>
        </nav>
        <button type="button" class="flex h-10 w-10 items-center justify-center border border-[#9a632c]/30 text-xl text-[#6b4327] md:hidden" aria-label="打开菜单" :aria-expanded="isMenuOpen" @click="isMenuOpen = !isMenuOpen">
          <span aria-hidden="true">{{ isMenuOpen ? '×' : '☰' }}</span>
        </button>
      </div>
      <nav v-if="isMenuOpen" class="border-t border-[#b58b54]/25 px-6 pb-5 pt-3 md:hidden" aria-label="移动端主导航">
        <NuxtLink v-for="item in navigation" :key="item.href" :to="item.href" class="block border-b border-[#b58b54]/15 py-3 text-sm text-[#715744]" @click="closeMenu">{{ item.label }}</NuxtLink>
      </nav>
    </header>

    <main>
      <section class="relative mx-auto max-w-7xl px-6 pb-24 pt-24 lg:px-10 lg:pb-32 lg:pt-36">
        <!-- 右侧图片 + 线框装饰 -->
  <div class="absolute right-4 top-10 hidden lg:block lg:right-10">
    <div class="relative">
      <!-- 外层线框 -->
      <div class="absolute -inset-4 rounded-full border border-[#b58b54]/30"></div>
      <!-- 图片 -->
      <img src="https://images.pexels.com/photos/30770256/pexels-photo-30770256.jpeg" alt="毛南族非遗工艺" class="h-[400px] w-[400px] rounded-full object-cover shadow-xl lg:h-[480px] lg:w-[480px]" />
      <!-- 内层小线框装饰 -->
      <div class="absolute -bottom-6 -left-6 h-24 w-24 rounded-full border border-[#b58b54]/20"></div>
    </div>
  </div>
  <div class="relative max-w-3xl">
          <p class="mb-7 text-xs font-medium uppercase tracking-[0.38em] text-[#9a632c]">Huanjiang · Molao Heritage</p>
          <h1 class="max-w-2xl font-serif text-5xl font-bold leading-[1.12] tracking-[0.08em] text-[#452b1d] sm:text-6xl lg:text-8xl">织锦传韵<br><span class="text-[#9a632c]">·美物焕新</span></h1>
          <p class="mt-8 max-w-xl text-base leading-8 text-[#715744] sm:text-lg">环江毛南族非遗服饰与装饰用品的数字出海赋能路</p>
          <NuxtLink to="/products" class="mt-10 inline-flex items-center gap-5 bg-[#6b4327] px-7 py-4 text-sm font-medium tracking-[0.18em] text-[#fffaf2] transition-colors hover:bg-[#9a632c]">探索产品 <span aria-hidden="true">↗</span></NuxtLink>
        </div>
        <div class="relative mt-16 flex items-center gap-4 text-xs tracking-[0.2em] text-[#9a632c] lg:absolute lg:bottom-20 lg:right-10 lg:mt-0"><span class="h-px w-12 bg-[#b58b54]"></span><span>TRADITION / CONTEMPORARY</span></div>
      </section>

      <section class="border-y border-[#b58b54]/25 bg-[#efe2cf]" aria-labelledby="category-title">
        <div class="mx-auto max-w-7xl px-6 py-20 lg:px-10 lg:py-24">
          <div class="mb-12 flex flex-col justify-between gap-4 sm:flex-row sm:items-end"><div><p class="mb-3 text-xs uppercase tracking-[0.3em] text-[#9a632c]">Curated Collection</p><h2 id="category-title" class="font-serif text-3xl font-bold tracking-[0.08em] text-[#452b1d] sm:text-4xl">从一顶花竹帽开始</h2></div><p class="max-w-xs text-sm leading-7 text-[#826a56]">三类文化产品，连接传统手艺与当代生活。</p></div>
          <div class="grid gap-5 md:grid-cols-3">
            <NuxtLink v-for="category in categories" :key="category.slug" :to="{ path: '/products', query: { category: category.slug } }" class="group border border-[#b58b54]/35 bg-[#f8f1e5] p-7 transition-all hover:-translate-y-1 hover:border-[#9a632c]"><div class="mb-16 flex h-14 w-14 items-center justify-center border border-[#9a632c]/50 font-serif text-2xl text-[#9a632c]">{{ category.icon }}</div><h3 class="font-serif text-2xl font-bold text-[#452b1d]">{{ category.name }}</h3><p class="mt-4 min-h-14 text-sm leading-7 text-[#826a56]">{{ category.description }}</p><span class="mt-7 inline-block text-sm text-[#9a632c] transition-transform group-hover:translate-x-2" aria-hidden="true">查看系列 →</span></NuxtLink>
          </div>
        </div>
      </section>

      <section class="mx-auto max-w-7xl px-6 py-20 lg:px-10 lg:py-28" aria-labelledby="highlight-title">
        <div class="mb-12"><p class="mb-3 text-xs uppercase tracking-[0.3em] text-[#9a632c]">Our Approach</p><h2 id="highlight-title" class="font-serif text-3xl font-bold tracking-[0.08em] text-[#452b1d] sm:text-4xl">让文化被看见，也被需要</h2></div>
        <div class="grid gap-10 border-t border-[#b58b54]/30 pt-8 md:grid-cols-3"><div v-for="highlight in highlights" :key="highlight.title" class="flex gap-5"><span class="font-serif text-3xl text-[#9a632c]">{{ highlight.icon }}</span><div><h3 class="font-serif text-xl font-bold text-[#452b1d]">{{ highlight.title }}</h3><p class="mt-2 text-sm leading-7 text-[#826a56]">{{ highlight.description }}</p></div></div></div>
      </section>

      <section class="mx-auto max-w-7xl px-6 pb-20 lg:px-10 lg:pb-28" aria-labelledby="craft-title">
        <div class="relative flex min-h-[25rem] items-end overflow-hidden bg-[#59402e] p-8 sm:p-12"><div class="absolute inset-0 opacity-60" style="background-image: linear-gradient(135deg, transparent 0 48%, #b58b54 48% 49%, transparent 49% 100%), repeating-linear-gradient(45deg, transparent 0 18px, rgba(248, 241, 229, .12) 19px 20px); background-size: 190px 190px, 34px 34px;" aria-hidden="true"></div><div class="relative z-10"><p class="mb-4 text-xs uppercase tracking-[0.35em] text-[#e5bc78]">Watch the craft</p><h2 id="craft-title" class="font-serif text-4xl font-bold tracking-[0.08em] text-[#fffaf2] sm:text-5xl">一针一线皆传承</h2><div class="mt-8 flex h-12 w-12 items-center justify-center border border-[#e5bc78] text-xl text-[#e5bc78]" aria-label="播放工艺视频占位">▶</div></div><span class="absolute right-8 top-8 text-xs tracking-[0.3em] text-[#e5bc78]">CRAFT / 01</span></div>
      </section>

      <section class="border-y border-[#b58b54]/25 bg-[#efe2cf] px-6 py-6 text-center text-xs tracking-[0.12em] text-[#715744] lg:px-10">🌏 Target Markets: Japan · Korea · Singapore · Malaysia · Vietnam · Thailand</section>
    </main>

    <footer class="mx-auto flex max-w-7xl flex-col gap-3 px-6 py-10 text-sm text-[#826a56] sm:flex-row sm:items-center sm:justify-between lg:px-10"><p>© 2026 织锦传韵·美物焕新. All rights reserved.</p><a href="mailto:hello@zhijinchuanyun.com" class="transition-colors hover:text-[#9a632c]">hello@zhijinchuanyun.com</a></footer>
  </div>
</template>