<script setup lang="ts">
const isMenuOpen = ref(false)

const navigation = [
  { label: '首页', href: '/' },
  { label: '产品', href: '/products' },
]

const products = [
  { id: 1, name_cn: '毛南族传统织锦头饰', name_en: 'Maonan Traditional Brocade Headdress', category: '服饰饰品', desc: '以红、黄、蓝三色丝线手工织造，纹样承载毛南族祈福图腾', image_bg: '#B8956A' },
  { id: 2, name_cn: '毛南族织锦围巾', name_en: 'Maonan Brocade Scarf', category: '服饰饰品', desc: '柔软羊毛为底，手工织锦纹样点缀，兼具保暖与文化寓意', image_bg: '#B8956A' },
  { id: 3, name_cn: '经典花竹帽', name_en: 'Classic Bamboo Flower Hat', category: '花竹帽IP', desc: '环江毛南族标志性器物，竹篾精细编织，象征爱情与吉祥', image_bg: '#4A6741' },
  { id: 4, name_cn: '花竹帽IP盲盒', name_en: 'Bamboo Hat IP Blind Box', category: '花竹帽IP', desc: '以花竹帽为原型设计的潮玩盲盒系列，传统符号年轻化表达', image_bg: '#4A6741' },
  { id: 5, name_cn: '非遗纹样帆布袋', name_en: 'Cultural Pattern Tote Bag', category: '文创衍生', desc: '提取毛南族织锦经典纹样，印于环保帆布包上，日常实用', image_bg: '#8B5A2B' },
  { id: 6, name_cn: '毛南香包挂件', name_en: 'Maonan Sachet Pendant', category: '文创衍生', desc: '传统香囊工艺结合毛南族图腾，天然草药填充，驱蚊安神', image_bg: '#8B5A2B' }
]

const categories = ['全部', '服饰饰品', '花竹帽IP', '文创衍生']
const selectedCategory = ref('全部')

// 从 URL 获取初始分类
const route = useRoute()
onMounted(() => {
  if (route.query.category) {
    const categoryMap: Record<string, string> = {
      'fashion': '服饰饰品',
      'flower-bamboo-hat': '花竹帽IP',
      'cultural-creative': '文创衍生'
    }
    const category = categoryMap[route.query.category as string]
    if (category) {
      selectedCategory.value = category
    }
  }
})

const filteredProducts = computed(() => {
  if (selectedCategory.value === '全部') {
    return products
  }
  return products.filter(product => product.category === selectedCategory.value)
})

const closeMenu = () => {
  isMenuOpen.value = false
}
</script>

<template>
  <div class="min-h-screen bg-[#FDF8F3] text-[#5D4037]">
    <!-- 顶部导航栏 -->
    <header class="relative z-20 border-b border-[#B8956A]/30 bg-[#FDF8F3]/95 backdrop-blur">
      <div class="mx-auto flex max-w-7xl items-center justify-between px-6 py-5 lg:px-10">
        <NuxtLink to="/" class="font-serif text-lg font-bold tracking-[0.12em] text-[#5D4037]" @click="closeMenu">织锦传韵·美物焕新</NuxtLink>
        <nav class="hidden items-center gap-8 text-sm text-[#5D4037] md:flex" aria-label="主导航">
          <NuxtLink v-for="item in navigation" :key="item.href" :to="item.href"
            class="transition-colors hover:text-[#B8956A] relative"
            :class="{ 'text-[#B8956A]': item.label === '产品' }">
            {{ item.label }}
            <span v-if="item.label === '产品'" class="absolute -bottom-1 left-0 right-0 h-0.5 bg-[#B8956A]"></span>
          </NuxtLink>
        </nav>
        <button type="button" class="flex h-10 w-10 items-center justify-center border border-[#5D4037]/30 text-xl text-[#5D4037] md:hidden" aria-label="打开菜单" :aria-expanded="isMenuOpen" @click="isMenuOpen = !isMenuOpen">
          <span aria-hidden="true">{{ isMenuOpen ? '×' : '☰' }}</span>
        </button>
      </div>
      <nav v-if="isMenuOpen" class="border-t border-[#B8956A]/30 px-6 pb-5 pt-3 md:hidden" aria-label="移动端主导航">
        <NuxtLink v-for="item in navigation" :key="item.href" :to="item.href" class="block border-b border-[#B8956A]/20 py-3 text-sm text-[#5D4037]" @click="closeMenu">{{ item.label }}</NuxtLink>
      </nav>
    </header>

    <!-- 页面标题区 -->
    <section class="relative mx-auto max-w-7xl px-6 py-16 lg:px-10">
      <div class="text-center">
        <h1 class="font-serif text-4xl font-bold tracking-[0.08em] text-[#5D4037] sm:text-5xl lg:text-6xl">产品展示</h1>
        <p class="mt-4 text-xl font-medium tracking-[0.15em] text-[#B8956A] uppercase">Cultural Products</p>
        <p class="mt-4 max-w-xl mx-auto text-base leading-7 text-[#5D4037]">探索毛南族非遗手工艺之美</p>
      </div>
    </section>

    <!-- 分类筛选 Tab -->
    <section class="border-b border-[#B8956A]/20 bg-white/50">
      <div class="mx-auto max-w-7xl px-6 py-4 lg:px-10">
        <div class="flex gap-3 overflow-x-auto">
          <button v-for="category in categories" :key="category"
            @click="selectedCategory = category"
            class="whitespace-nowrap px-5 py-2.5 rounded-full text-sm font-medium transition-all"
            :class="selectedCategory === category
              ? 'bg-[#5D4037] text-white shadow-md'
              : 'bg-[#FDF8F3] text-[#5D4037] hover:bg-[#FDF8F3] border border-[#5D4037]/20'">
            {{ category }}
          </button>
        </div>
      </div>
    </section>

    <!-- 产品卡片网格 -->
    <main class="mx-auto max-w-7xl px-6 py-12 lg:px-10">
      <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-3">
        <NuxtLink v-for="product in filteredProducts" :key="product.id" to="/products"
          class="group rounded-xl bg-white p-4 shadow-md transition-all duration-300 hover:-translate-y-1 hover:shadow-lg">
          <!-- 图片区域 -->
          <div class="mb-4 h-48 rounded-lg flex items-center justify-center text-5xl font-serif font-bold"
            :style="{ backgroundColor: product.image_bg }">
            {{ product.category[0] }}
          </div>

          <!-- 品类标签 -->
          <div class="absolute top-4 right-4">
            <span class="inline-block rounded-full px-3 py-1 text-xs font-medium"
              :style="{ backgroundColor: product.image_bg + '20', color: product.image_bg }">
              {{ product.category }}
            </span>
          </div>

          <!-- 产品信息 -->
          <div class="relative">
            <h3 class="font-serif text-xl font-bold text-[#5D4037]">{{ product.name_cn }}</h3>
            <p class="mt-1 text-sm text-gray-500">{{ product.name_en }}</p>
            <p class="mt-3 text-sm text-[#5D4037]/70 leading-relaxed">{{ product.desc }}</p>
            <div class="mt-4 flex items-center text-sm font-medium text-[#B8956A] group-hover:translate-x-1 transition-transform">
              查看详情
              <span aria-hidden="true" class="ml-2">→</span>
            </div>
          </div>
        </NuxtLink>
      </div>
    </main>

    <!-- 页脚 -->
    <footer class="mx-auto max-w-7xl border-t border-[#B8956A]/20 px-6 py-8 text-center text-sm text-[#5D4037]/60 lg:px-10">
      <p>© 2026 织锦传韵·美物焕新. All rights reserved.</p>
      <a href="mailto:hello@zhijinchuanyun.com" class="mt-2 inline-block text-[#5D4037]/60 hover:text-[#B8956A] transition-colors">hello@zhijinchuanyun.com</a>
    </footer>
  </div>
</template>
