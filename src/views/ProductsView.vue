<template>
  <section class="container py-3">
    <header class="text-center mb-3">
      <h2 class="h3">Kategoriler</h2>
      <p class="text-secondary">Diyarbakır'ın ruhunu taşıyan seçkilerimiz arasından dilediğinizi keşfedin.</p>
    </header>

    <ul class="nav nav-pills justify-content-center flex-wrap gap-2 mb-3">
      <li class="nav-item" v-for="c in categories" :key="c.id">
        <button class="nav-link" :class="{ active: c.id === selectedId }" @click="selectedId = c.id">{{ c.name }}</button>
      </li>
    </ul>

    <div v-if="current" class="banner mb-3 rounded-3" :style="{ backgroundImage: `url(${current.cover})` }">
      <div class="banner-overlay">
        <h3 class="h4 m-0">{{ current.name }}</h3>
        <span class="small">Seçkiden örnekler</span>
      </div>
    </div>

    <div class="row g-3">
      <article v-for="(img,idx) in (current?.items || [])" :key="idx" class="col-6 col-md-4 col-lg-3">
        <div class="card h-100 shadow-sm">
          <div class="ratio ratio-4x3" :style="{ background: `url(${img}) center/cover no-repeat` }"></div>
          <div class="card-body py-2">
            <h3 class="h6 m-0">{{ current?.name }}</h3>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from 'vue'

interface Category {
  id: string;
  name: string;
  cover: string;
  items: string[];
}

export default defineComponent({
  name: 'ProductsView',
  setup() {
    const categories = ref<Category[]>([
      {
        id: 'guller',
        name: 'Güller',
        cover: 'https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1470137430626-983a37b8ea46?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1481241992364-5cabe57bb0a0?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1514514805403-b9439be04b20?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1509043759401-136742328bb3?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'orkideler',
        name: 'Orkideler',
        cover: 'https://images.unsplash.com/photo-1542259009477-98a5a5a3327b?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1542259009477-98a5a5a3327b?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1531219432768-9f540ce91ef3?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1519682337058-a94d519337bc?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1520975922217-7b683d8b62a0?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1520722350857-1e0e3f8c2f5f?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'saksi',
        name: 'Saksı Çiçekleri',
        cover: 'https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1484980859177-5ac1249fda6f?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1446071103084-c257b5f70672?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1488521787991-ed7bbaae773c?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'acilis',
        name: 'Açılış Çiçekleri',
        cover: 'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1519682337058-a94d519337bc?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1514514805403-b9439be04b20?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1509043759401-136742328bb3?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1481241992364-5cabe57bb0a0?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'celenk',
        name: 'Çelenkler',
        cover: 'https://images.unsplash.com/photo-1509043759401-136742328bb3?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1509043759401-136742328bb3?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1481241992364-5cabe57bb0a0?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1514514805403-b9439be04b20?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'buketler',
        name: 'Buketler',
        cover: 'https://images.unsplash.com/photo-1470137430626-983a37b8ea46?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1470137430626-983a37b8ea46?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1481241992364-5cabe57bb0a0?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1509043759401-136742328bb3?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1514514805403-b9439be04b20?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'papatyalar',
        name: 'Papatyalar',
        cover: 'https://images.unsplash.com/photo-1436891620584-47fd0e565afb?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1436891620584-47fd0e565afb?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1468327768560-75b778cbb551?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1509043759401-136742328bb3?q=80&w=1000&auto=format&fit=crop',
        ]
      },
      {
        id: 'cikolatalar',
        name: 'Çikolatalar',
        cover: 'https://images.unsplash.com/photo-1454678904372-2c7b04a237f1?q=80&w=1200&auto=format&fit=crop',
        items: [
          'https://images.unsplash.com/photo-1534422298391-e4f8c172dddb?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1511381939415-c1c76e2290c3?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1578985545062-69928b1d9587?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1504674900247-0877df9cc836?q=80&w=1000&auto=format&fit=crop',
          'https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1000&auto=format&fit=crop',
        ]
      },
    ])

    const selectedId = ref<string>('guller')
    const current = computed(() => categories.value.find(c => c.id === selectedId.value))

    return { categories, selectedId, current }
  }
})
</script>

<style scoped>
.ratio { border-top-left-radius: .5rem; border-top-right-radius: .5rem; }
.banner { height: 220px; background: #eee center/cover no-repeat; position: relative; overflow: hidden; }
.banner::after { content:""; position:absolute; inset:0; background: linear-gradient(0deg, rgba(0,0,0,.35), rgba(0,0,0,.05)); }
.banner-overlay { position:absolute; left:16px; bottom:12px; color:#fff; z-index:1; }
</style>


