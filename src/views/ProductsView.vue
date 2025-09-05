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
      <img v-if="bannerLeft" :src="bannerLeft" alt="" class="banner-fig left" />
      <img v-if="bannerRight" :src="bannerRight" alt="" class="banner-fig right" />
      <div class="banner-overlay">
        <h3 class="h4 m-0">{{ current.name }}</h3>
        <span class="small">Seçkiden örnekler</span>
      </div>
    </div>

    <div class="row g-3">
      <article v-for="(img,idx) in (current?.items || [])" :key="idx" class="col-6 col-md-4 col-lg-3">
        <div class="card h-100 shadow-sm">
          <a href="#" class="preview" data-bs-toggle="modal" data-bs-target="#imgModal" @click.prevent="openPreview(idx)">
            <div class="ratio ratio-4x3" :style="{ background: `url(${img}) center/cover no-repeat` }"></div>
          </a>
          <div class="card-body py-2">
            <div class="card-meta">
              <span class="pill">{{ current?.name }}</span>
              <span class="muted">Örnek {{ idx + 1 }}</span>
            </div>
          </div>
        </div>
      </article>
    </div>

    <div class="modal fade" id="imgModal" tabindex="-1" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered modal-xl">
        <div class="modal-content bg-dark border-0">
          <button type="button" class="btn-close btn-close-white ms-auto me-2 mt-2" data-bs-dismiss="modal" aria-label="Close"></button>
          <div id="galleryCarousel" class="carousel slide" data-bs-interval="false">
            <div class="carousel-inner">
              <div v-for="(img, i) in (current?.items || [])" :key="i" class="carousel-item" :class="{ active: i === selectedIndex }">
                <div class="zoom-wrap">
                  <img :src="img" class="d-block w-100 rounded-3" alt="Görsel" />
                </div>
              </div>
            </div>
            <button class="carousel-control-prev" type="button" data-bs-target="#galleryCarousel" data-bs-slide="prev">
              <span class="carousel-control-prev-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Önceki</span>
            </button>
            <button class="carousel-control-next" type="button" data-bs-target="#galleryCarousel" data-bs-slide="next">
              <span class="carousel-control-next-icon" aria-hidden="true"></span>
              <span class="visually-hidden">Sonraki</span>
            </button>
          </div>
          <div class="caption text-center text-white-50 py-2">
            {{ current?.name }} • {{ selectedIndex + 1 }}/{{ current?.items.length || 0 }}
          </div>
        </div>
      </div>
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
        cover: '/gul.jpeg',
        items: [
          '/guller/1.jpg',
          '/guller/2.jpg',
          '/guller/3.jpg',
          '/guller/4.jpg',
          '/guller/2.jpg'
        ]
      },
      {
        id: 'orkideler',
        name: 'Orkideler',
        cover: '/orkide.jpg',
        items: [
          '/orkideler/1.JPG',
          '/orkideler/2.JPG',
          '/orkideler/3.JPG',
          '/orkideler/4.JPG',
          '/orkideler/5.JPG',
        ]
      },
      {
        id: 'saksi',
        name: 'Saksı Çiçekleri',
        cover: '/saksicicekleri.jpg',
        items: [
          '/saksiCicekleri/1.JPG',
          '/saksiCicekleri/2.JPG',
          '/saksiCicekleri/3.JPG',
          '/saksiCicekleri/4.JPG',
          '/saksiCicekleri/5.JPG',
        ]
      },
      {
        id: 'acilis',
        name: 'Açılış Çiçekleri',
        cover: '/aciliscicekleri.jpg',
        items: [
          '/acilisCicekleri/IMG_4365.JPG',
          '/acilisCicekleri/IMG_4366.JPG',
          '/acilisCicekleri/IMG_4369.JPG',
          '/acilisCicekleri/IMG_4370.JPG',
          '/acilisCicekleri/IMG_4371.JPG',
        ]
      },
      {
        id: 'celenk',
        name: 'Çelenkler',
        cover: '/celenk.jpg',
        items: [
          '/celenkler/1.JPG',
          '/celenkler/2.JPG',
          '/celenkler/3.JPG',
          '/celenkler/4.JPG',
          '/celenkler/5.JPG',
        ]
      },
      {
        id: 'buketler',
        name: 'Buketler',
        cover: '/buket.jpg',
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
        cover: '/papatya.jpg',
        items: [
          '/papatyalar/1.JPG',
          '/papatyalar/2.JPG',
          '/papatyalar/3.JPG',
          '/papatyalar/1.JPG',
          '/papatyalar/2.JPG',
        ]
      },
      {
        id: 'cikolatalar',
        name: 'Çikolatalar',
        cover: '/cikolata.jpg',
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
    const bannerLeft = computed(() => current.value ? current.value.items[0] : '')
    const bannerRight = computed(() => current.value ? current.value.items[1] : '')

    const selectedIndex = ref<number>(0)
    const selectedImage = ref<string>('')
    const openPreview = (idx: number) => {
      selectedIndex.value = idx
      selectedImage.value = current.value?.items[idx] || ''
    }
    return { categories, selectedId, current, selectedImage, selectedIndex, openPreview, bannerLeft, bannerRight }
  }
})
</script>

<style scoped>
.ratio { border-top-left-radius: .5rem; border-top-right-radius: .5rem; background-position: 50% 35% !important; }
.banner { height: 240px; background: #eee center/cover no-repeat; background-position: 50% 35%; position: relative; overflow: hidden; }
.banner::after { content:""; position:absolute; inset:0; background: linear-gradient(0deg, rgba(0,0,0,.35), rgba(0,0,0,.05)); }
.banner-overlay { position:absolute; left:16px; bottom:12px; color:#fff; z-index:1; }
.banner-fig { position:absolute; top:50%; transform: translateY(-50%) rotate(-4deg); width: 150px; height: 110px; object-fit: cover; border-radius: 12px; box-shadow: 0 6px 18px rgba(0,0,0,.2); border: 2px solid rgba(255,255,255,.7); }
.banner-fig.right { right: 12px; transform: translateY(-50%) rotate(6deg); }
.banner-fig.left { left: 12px; }
.nav-pills .nav-link { border:1px solid #111; color:#111; background:#fff; }
.nav-pills .nav-link.active { background:#111; color:#fff; }
.preview { display:block; }
.preview .ratio { transition: transform .25s ease; }
.preview:hover .ratio { transform: scale(1.02); }
.modal-content { border-radius: 16px; overflow: hidden; }
.zoom-wrap { overflow: hidden; }
.zoom-wrap img { transition: transform .35s ease; }
.zoom-wrap img:hover { transform: scale(1.03); }
.card-meta { display:flex; align-items:center; justify-content:space-between; }
.pill { border:1px solid #111; border-radius:999px; padding:2px 8px; font-size:12px; font-weight:700; letter-spacing:.3px; }
.muted { color:#6c757d; font-size:12px; }
</style>


