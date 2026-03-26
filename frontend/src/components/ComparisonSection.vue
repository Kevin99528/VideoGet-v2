<template>
  <section id="comparison" class="py-16 md:py-24 bg-gradient-to-b from-slate-50 to-white">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <!-- SEO 优化标题区域 -->
      <header class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold text-slate-800 mb-4">
          视频下载器对比：VideoGet vs 其他工具
        </h2>
        <p class="text-slate-600 text-lg max-w-3xl mx-auto">
          寻找最好的 YouTube 视频下载工具？我们对比了市面上主流的视频下载软件，
          从支持平台、画质、速度、价格等多个维度，帮你找到最适合的解决方案。
        </p>
      </header>

      <!-- 对比表格 -->
      <div class="bg-white rounded-2xl shadow-xl overflow-hidden border border-slate-200">
        <!-- 桌面端表格 -->
        <div class="hidden md:block overflow-x-auto">
          <table class="w-full">
            <thead>
              <tr class="bg-gradient-to-r from-blue-600 to-blue-700 text-white">
                <th class="px-6 py-4 text-left font-semibold">对比维度</th>
                <th class="px-6 py-4 text-center font-bold bg-blue-800">VideoGet</th>
                <th class="px-6 py-4 text-center">4K Video Downloader</th>
                <th class="px-6 py-4 text-center">Y2mate</th>
                <th class="px-6 py-4 text-center">SaveFrom.net</th>
                <th class="px-6 py-4 text-center">ByClick Downloader</th>
              </tr>
            </thead>
            <tbody class="divide-y divide-slate-200">
              <tr v-for="(row, index) in comparisonData" :key="index" 
                  :class="index % 2 === 0 ? 'bg-white' : 'bg-slate-50'">
                <td class="px-6 py-4 font-medium text-slate-800">{{ row.dimension }}</td>
                <td class="px-6 py-4 text-center bg-blue-50">
                  <span :class="getVideoGetClass(row.videoGet)">{{ row.videoGet }}</span>
                </td>
                <td class="px-6 py-4 text-center text-slate-600">{{ row.competitor1 }}</td>
                <td class="px-6 py-4 text-center text-slate-600">{{ row.competitor2 }}</td>
                <td class="px-6 py-4 text-center text-slate-600">{{ row.competitor3 }}</td>
                <td class="px-6 py-4 text-center text-slate-600">{{ row.competitor4 }}</td>
              </tr>
            </tbody>
          </table>
        </div>

        <!-- 移动端卡片布局 -->
        <div class="md:hidden">
          <div v-for="(product, pIndex) in mobileComparisonData" :key="pIndex" 
               class="border-b border-slate-200 last:border-b-0"
               :class="product.isVideoGet ? 'bg-blue-50' : 'bg-white'">
            <div class="px-4 py-3 font-bold text-lg" 
                 :class="product.isVideoGet ? 'text-blue-700 bg-blue-100' : 'text-slate-800 bg-slate-100'">
              {{ product.name }}
            </div>
            <div class="px-4 py-2 space-y-2">
              <div v-for="(item, iIndex) in product.features" :key="iIndex" 
                   class="flex justify-between py-1 border-b border-slate-100 last:border-b-0">
                <span class="text-slate-600 text-sm">{{ item.label }}</span>
                <span :class="item.isHighlight ? 'text-blue-600 font-semibold' : 'text-slate-800'">
                  {{ item.value }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- 核心优势总结 -->
      <div class="mt-12 grid grid-cols-1 md:grid-cols-3 gap-6">
        <article class="bg-white p-6 rounded-xl shadow-lg border border-blue-100 hover:shadow-xl transition-shadow">
          <div class="w-12 h-12 rounded-lg bg-blue-100 flex items-center justify-center mb-4">
            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"/>
            </svg>
          </div>
          <h3 class="text-lg font-bold text-slate-800 mb-2">完全免费使用</h3>
          <p class="text-slate-600">
            VideoGet 提供免费版本，无需付费即可下载高清视频。相比 4K Video Downloader 的付费限制，
            我们让用户零成本享受优质服务。
          </p>
        </article>

        <article class="bg-white p-6 rounded-xl shadow-lg border border-blue-100 hover:shadow-xl transition-shadow">
          <div class="w-12 h-12 rounded-lg bg-blue-100 flex items-center justify-center mb-4">
            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"/>
            </svg>
          </div>
          <h3 class="text-lg font-bold text-slate-800 mb-2">极速下载体验</h3>
          <p class="text-slate-600">
            采用多线程加速技术，下载速度比 Y2mate 和 SaveFrom.net 等在线工具快 3-5 倍，
            大文件也能秒速下载。
          </p>
        </article>

        <article class="bg-white p-6 rounded-xl shadow-lg border border-blue-100 hover:shadow-xl transition-shadow">
          <div class="w-12 h-12 rounded-lg bg-blue-100 flex items-center justify-center mb-4">
            <svg class="w-6 h-6 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"/>
            </svg>
          </div>
          <h3 class="text-lg font-bold text-slate-800 mb-2">AI 智能功能</h3>
          <p class="text-slate-600">
            独家提供 AI 视频总结和字幕翻译功能，这是其他下载工具都不具备的智能特性，
            让视频内容更易理解和传播。
          </p>
        </article>
      </div>

      <!-- SEO 关键词区域 -->
      <footer class="mt-12 text-center">
        <div class="inline-flex flex-wrap justify-center gap-2 text-sm text-slate-500">
          <span>相关搜索：</span>
          <span class="px-3 py-1 bg-slate-100 rounded-full">视频下载器对比</span>
          <span class="px-3 py-1 bg-slate-100 rounded-full">YouTube下载工具</span>
          <span class="px-3 py-1 bg-slate-100 rounded-full">免费视频下载软件</span>
          <span class="px-3 py-1 bg-slate-100 rounded-full">在线视频下载</span>
          <span class="px-3 py-1 bg-slate-100 rounded-full">4K视频下载</span>
          <span class="px-3 py-1 bg-slate-100 rounded-full">批量下载视频</span>
        </div>
      </footer>
    </div>
  </section>
</template>

<script setup>
// 桌面端对比数据
const comparisonData = [
  {
    dimension: '支持平台',
    videoGet: '1800+ 平台',
    competitor1: '30+ 平台',
    competitor2: '50+ 平台',
    competitor3: '40+ 平台',
    competitor4: '50+ 平台'
  },
  {
    dimension: '最高画质',
    videoGet: '8K 超高清',
    competitor1: '4K 高清',
    competitor2: '1080P',
    competitor3: '1080P',
    competitor4: '4K 高清'
  },
  {
    dimension: '下载速度',
    videoGet: '⭐⭐⭐⭐⭐ 极速',
    competitor1: '⭐⭐⭐⭐ 快速',
    competitor2: '⭐⭐⭐ 一般',
    competitor3: '⭐⭐⭐ 一般',
    competitor4: '⭐⭐⭐⭐ 快速'
  },
  {
    dimension: '批量下载',
    videoGet: '✅ 支持',
    competitor1: '✅ 支持',
    competitor2: '❌ 不支持',
    competitor3: '❌ 不支持',
    competitor4: '✅ 支持'
  },
  {
    dimension: '价格',
    videoGet: '免费',
    competitor1: '¥159/年',
    competitor2: '免费（广告多）',
    competitor3: '免费（广告多）',
    competitor4: '¥199/年'
  },
  {
    dimension: 'AI 视频总结',
    videoGet: '✅ 支持',
    competitor1: '❌ 不支持',
    competitor2: '❌ 不支持',
    competitor3: '❌ 不支持',
    competitor4: '❌ 不支持'
  },
  {
    dimension: '字幕翻译',
    videoGet: '✅ 支持',
    competitor1: '❌ 不支持',
    competitor2: '❌ 不支持',
    competitor3: '❌ 不支持',
    competitor4: '❌ 不支持'
  },
  {
    dimension: '使用方式',
    videoGet: '网页在线',
    competitor1: '软件安装',
    competitor2: '网页在线',
    competitor3: '网页在线',
    competitor4: '软件安装'
  }
]

// 移动端对比数据
const mobileComparisonData = [
  {
    name: 'VideoGet',
    isVideoGet: true,
    features: [
      { label: '支持平台', value: '1800+', isHighlight: true },
      { label: '最高画质', value: '8K', isHighlight: true },
      { label: '下载速度', value: '极速', isHighlight: true },
      { label: '批量下载', value: '支持', isHighlight: true },
      { label: '价格', value: '免费', isHighlight: true },
      { label: 'AI 功能', value: '支持', isHighlight: true }
    ]
  },
  {
    name: '4K Video Downloader',
    isVideoGet: false,
    features: [
      { label: '支持平台', value: '30+', isHighlight: false },
      { label: '最高画质', value: '4K', isHighlight: false },
      { label: '下载速度', value: '快速', isHighlight: false },
      { label: '批量下载', value: '支持', isHighlight: false },
      { label: '价格', value: '¥159/年', isHighlight: false },
      { label: 'AI 功能', value: '不支持', isHighlight: false }
    ]
  },
  {
    name: 'Y2mate',
    isVideoGet: false,
    features: [
      { label: '支持平台', value: '50+', isHighlight: false },
      { label: '最高画质', value: '1080P', isHighlight: false },
      { label: '下载速度', value: '一般', isHighlight: false },
      { label: '批量下载', value: '不支持', isHighlight: false },
      { label: '价格', value: '免费(广告)', isHighlight: false },
      { label: 'AI 功能', value: '不支持', isHighlight: false }
    ]
  },
  {
    name: 'SaveFrom.net',
    isVideoGet: false,
    features: [
      { label: '支持平台', value: '40+', isHighlight: false },
      { label: '最高画质', value: '1080P', isHighlight: false },
      { label: '下载速度', value: '一般', isHighlight: false },
      { label: '批量下载', value: '不支持', isHighlight: false },
      { label: '价格', value: '免费(广告)', isHighlight: false },
      { label: 'AI 功能', value: '不支持', isHighlight: false }
    ]
  }
]

// 获取 VideoGet 单元格的样式类
function getVideoGetClass(value) {
  if (value.includes('✅') || value.includes('⭐⭐⭐⭐⭐') || value === '免费' || value === '8K 超高清' || value === '1800+ 平台') {
    return 'text-blue-600 font-bold'
  }
  return 'text-slate-800'
}
</script>
