<template>
  <section class="container py-3">
    <header class="text-center mb-3">
      <h2 class="h3">Diyarbakır Esintili Koleksiyon</h2>
      <p class="text-secondary">Hevsel'in yeşili, surların asaleti; tasarımlarımızda bir araya geliyor.</p>
    </header>

    <div class="row g-3">
      <article v-for="p in products" :key="p.id" class="col-sm-6 col-lg-3">
        <div class="card h-100 shadow-sm">
          <div class="ratio ratio-4x3" :style="{ background: `url(${p.image}) center/cover no-repeat` }"></div>
          <div class="card-body d-flex flex-column">
            <h3 class="h6 mb-1">{{ p.title }}</h3>
            <p class="text-secondary small mb-2">{{ p.description }}</p>
            <span class="fw-bold mt-auto">{{ p.price }} ₺</span>
          </div>
        </div>
      </article>
    </div>
  </section>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'

interface ProductItem {
  id: number;
  title: string;
  description: string;
  price: number;
  image: string;
}

export default defineComponent({
  name: 'ProductsView',
  setup() {
    const products = ref<ProductItem[]>([
      { id: 1, title: 'Pembe Gül Buketi', description: '12 adet pembe gül ve okaliptus', price: 950, image: 'https://images.unsplash.com/photo-1470137430626-983a37b8ea46?q=80&w=800&auto=format&fit=crop' },
      { id: 2, title: 'Beyaz Lilyum', description: 'Zarif beyaz lilyum aranjmanı', price: 780, image: 'https://images.unsplash.com/photo-1501004318641-b39e6451bec6?q=80&w=800&auto=format&fit=crop' },
      { id: 3, title: 'Renkli Kır Çiçekleri', description: 'Doğal ve canlı kır çiçekleri', price: 690, image: 'https://images.unsplash.com/photo-1490750967868-88aa4486c946?q=80&w=800&auto=format&fit=crop' },
      { id: 4, title: 'Orkide', description: 'Şık seramik saksıda orkide', price: 1150, image: 'https://images.unsplash.com/photo-1542259009477-98a5a5a3327b?q=80&w=800&auto=format&fit=crop' },
    ])
    return { products }
  }
})
</script>

<style scoped>
.ratio { border-top-left-radius: .5rem; border-top-right-radius: .5rem; }
</style>


