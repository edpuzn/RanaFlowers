<template>
  <section class="container py-3">
    <header class="text-center mb-3">
      <h2 class="h3">Kategoriler</h2>
      <p class="text-secondary">Diyarbakır'ın ruhunu taşıyan seçkilerimiz arasından dilediğinizi keşfedin.</p>
    </header>

    <ul class="nav nav-pills justify-content-center flex-wrap gap-2 mb-3">
      <li class="nav-item" v-for="c in categories" :key="c.id">
        <router-link class="nav-link" :class="{ active: c.id === selectedId }" :to="{ path: '/urunler', query: { cat: c.id } }">{{ c.name }}</router-link>
      </li>
    </ul>

    <div v-if="current" class="banner mb-3 rounded-3">
      <transition name="banner-swipe" mode="out-in">
        <div :key="bannerImage" class="banner-bg" :style="{ backgroundImage: `url(${bannerImage})` }"></div>
      </transition>
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
            <div class="ratio ratio-9x16" :style="{ background: `url(${img}) center/cover no-repeat` }"></div>
            <div class="img-label">{{ current?.name }}</div>
          </a>
        </div>
      </article>
    </div>


    
    <div class="modal fade" id="imgModal" tabindex="-1" aria-hidden="true">
      <div class="modal-dialog modal-dialog-centered modal-xl">
        <div class="modal-content bg-dark border-0">
          <button type="button" class="btn-close btn-close-white ms-auto me-2 mt-2" data-bs-dismiss="modal" aria-label="Close"></button>
          <div id="galleryCarousel" class="carousel slide" data-bs-interval="false" ref="carouselRef">
            <div class="carousel-inner">
              <div v-for="(img, i) in (current?.items || [])" :key="i" class="carousel-item" :class="{ active: i === selectedIndex }">
                <div class="zoom-wrap">
                  <img :src="img" class="modal-photo d-block rounded-3" alt="Görsel" />
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
import { defineComponent, ref, computed, watchEffect, onMounted, onBeforeUnmount } from 'vue'
import { useRoute, useRouter } from 'vue-router'

interface Category {
  id: string;
  name: string;
  cover: string;
  items: string[];
}

export default defineComponent({
  name: 'ProductsView',
  setup() {
    const route = useRoute()
    const router = useRouter()
    const categories = ref<Category[]>([
      {
        id: 'guller',
        name: 'Güller',
        cover: '/gul.webp',
        items: [
          '/guller/1.webp',
          '/guller/2.webp',
          '/guller/3.webp',
          '/guller/4.webp'
        ]
      },
      {
        id: 'orkideler',
        name: 'Orkideler',
        cover: '/orkide.webp',
        items: [
          '/orkideler/1.webp',
          '/orkideler/2.webp',
          '/orkideler/3.webp',
          '/orkideler/4.webp',
          '/orkideler/5.webp',
        ]
      },
      {
        id: 'saksi',
        name: 'Saksı Çiçekleri',
        cover: '/saksicicekleri.webp',
        items: [
          '/saksiCicekleri/1.webp',
          '/saksiCicekleri/2.webp',
          '/saksiCicekleri/3.webp',
          '/saksiCicekleri/4.webp',
          '/saksiCicekleri/5.webp',
          '/saksiCicekleri/6.webp',
          '/saksiCicekleri/7.webp',
          '/saksiCicekleri/8.webp',
          '/saksiCicekleri/9.webp',
          '/saksiCicekleri/10.webp'
        ]
      },
      {
        id: 'acilis',
        name: 'Açılış Çiçekleri',
        cover: '/aciliscicekleri.webp',
        items: [
          '/acilisCicekleri/IMG_4365.webp',
          '/acilisCicekleri/IMG_4366.webp',
          '/acilisCicekleri/IMG_4369.webp',
          '/acilisCicekleri/IMG_4370.webp',
          '/acilisCicekleri/IMG_4371.webp',
          '/acilisCicekleri/IMG_4372.webp'
        ]
      },
      {
        id: 'celenk',
        name: 'Çelenkler',
        cover: '/celenk.webp',
        items: [
          '/celenkler/1.webp',
          '/celenkler/2.webp',
          '/celenkler/3.webp',
          '/celenkler/4.webp',
          '/celenkler/5.webp',
          '/celenkler/6.webp',
          '/celenkler/7.webp'
        ]
      },
      {
        id: 'buketler',
        name: 'Buketler',
        cover: '/buket.webp',
        items: [
          '/buketler/1.webp',
          '/buketler/2.webp',
          '/buketler/3.webp',
          '/buketler/4.webp',
          '/buketler/5.webp',
          '/buketler/6.webp'
        ]
      },
      {
        id: 'lux',
        name: 'Lüks Buketler',
        cover: '/luxBuketler/1.webp',
        items: [
          '/luxBuketler/1.webp',
          '/luxBuketler/2.webp',
          '/luxBuketler/3.webp',
          '/luxBuketler/4.webp',
          '/luxBuketler/5.webp',
          '/luxBuketler/6.webp',
          '/luxBuketler/7.webp',
          '/luxBuketler/8.webp',
          '/luxBuketler/9.webp',
          '/luxBuketler/10.webp',
          '/luxBuketler/11.webp',
          '/luxBuketler/12.webp',
          '/luxBuketler/13.webp',
          '/luxBuketler/14.webp',
          '/luxBuketler/15.webp',
          '/luxBuketler/16.webp',
          '/luxBuketler/17.webp',
          '/luxBuketler/18.webp',
          '/luxBuketler/19.webp'
        ]
      },
      {
        id: 'papatyalar',
        name: 'Papatyalar',
        cover: '/papatya.webp',
        items: [
          '/papatyalar/1.webp',
          '/papatyalar/2.webp',
          '/papatyalar/3.webp'
        ]
      },
      {
        id: 'cikolatalar',
        name: 'Çikolatalar',
        cover: '/cikolata.jpg',
        items: [
          '/Cikolatalar/1.webp',
          '/Cikolatalar/2.webp',
          '/Cikolatalar/3.webp',
          '/Cikolatalar/4.webp',
          '/Cikolatalar/5.webp',
          '/Cikolatalar/6.webp',
          '/Cikolatalar/7.webp',
          '/Cikolatalar/8.webp',
          '/Cikolatalar/9.webp'
        ]
      },
    ])

    const selectedId = ref<string>((route.query.cat as string) || 'guller')
    const current = computed(() => categories.value.find(c => c.id === selectedId.value))
    const bannerLeft = computed(() => current.value ? current.value.items[0] : '')
    const bannerRight = computed(() => current.value ? current.value.items[1] : '')
    const bannerIndex = ref<number>(0)
    const bannerImage = ref<string>('')
    let bannerTimer: number | undefined
    const resetBanner = () => {
      bannerIndex.value = 0
      bannerImage.value = current.value?.items[bannerIndex.value] || current.value?.cover || ''
      if (bannerTimer) window.clearInterval(bannerTimer)
      bannerTimer = window.setInterval(() => {
        const list = current.value?.items || []
        if (list.length === 0) return
        bannerIndex.value = (bannerIndex.value + 1) % list.length
        bannerImage.value = list[bannerIndex.value]
      }, 5000)
    }
    watchEffect(() => { if (current.value) resetBanner() })
    // URL query -> state sync
    watchEffect(() => {
      const q = (route.query.cat as string) || ''
      if (q && q !== selectedId.value) selectedId.value = q
    })
    // state -> URL query sync on change (without navigation)
    watchEffect(() => {
      router.replace({ query: { ...route.query, cat: selectedId.value } })
    })
    onMounted(() => resetBanner())
    onBeforeUnmount(() => { if (bannerTimer) window.clearInterval(bannerTimer) })

    const selectedIndex = ref<number>(0)
    const carouselRef = ref<HTMLElement | null>(null)
    const selectedImage = ref<string>('')
    const openPreview = (idx: number) => {
      selectedIndex.value = idx
      selectedImage.value = current.value?.items[idx] || ''
    }
    const syncIndexFromDom = () => {
      const root = carouselRef.value
      if (!root) return
      const items = Array.from(root.querySelectorAll('.carousel-item'))
      const activeIndex = items.findIndex(el => el.classList.contains('active'))
      if (activeIndex >= 0) selectedIndex.value = activeIndex
    }

    let onSlid: ((e: Event) => void) | null = null
    onMounted(() => {
      const root = carouselRef.value
      if (!root) return
      const handler = () => syncIndexFromDom()
      onSlid = handler
      root.addEventListener('slid.bs.carousel', handler)
    })
    onBeforeUnmount(() => {
      const root = carouselRef.value
      if (root && onSlid) root.removeEventListener('slid.bs.carousel', onSlid)
    })

    return { categories, selectedId, current, selectedImage, selectedIndex, openPreview, bannerLeft, bannerRight, bannerImage, carouselRef }
  }
})
</script>

<style scoped>
.ratio { border-top-left-radius: .5rem; border-top-right-radius: .5rem; background-position: 50% 50% !important; }
.banner { height: 240px; position: relative; overflow: hidden; border-radius: 16px; }
.banner-bg { position:absolute; inset:0; background: #eee center/cover no-repeat; background-position: 50% 50%; }
.banner::after { content:""; position:absolute; inset:0; background: linear-gradient(0deg, rgba(0,0,0,.35), rgba(0,0,0,.05)); }
.banner-overlay { position:absolute; left:16px; bottom:12px; color:#fff; z-index:1; }
.banner-fig { position:absolute; top:50%; transform: translateY(-50%) rotate(-4deg); width: 150px; height: 110px; object-fit: cover; border-radius: 12px; box-shadow: 0 6px 18px rgba(0,0,0,.2); border: 2px solid rgba(255,255,255,.7); }
.banner-fig.right { right: 12px; transform: translateY(-50%) rotate(6deg); }
.banner-fig.left { left: 12px; }
.banner-swipe-enter-active, .banner-swipe-leave-active { transition: transform .6s cubic-bezier(.22,.61,.36,1); }
.banner-swipe-enter-from { transform: translateX(100%); }
.banner-swipe-leave-to { transform: translateX(-100%); }
.nav-pills .nav-link { border:1px solid #111; color:#111; background:#fff; }
.nav-pills .nav-link.active { background:#111; color:#fff; }
.preview { display:block; }
.preview .ratio { transition: transform .25s ease; }
.preview:hover .ratio { transform: scale(1.02); }
.img-label { position:absolute; left:10px; bottom:8px; color:#fff; font-weight:800; font-size:12px; letter-spacing:.5px; text-shadow:0 2px 8px rgba(0,0,0,.6), 0 1px 2px rgba(0,0,0,.5); padding:2px 6px; border-radius:8px; }
.modal-content { border-radius: 16px; overflow: hidden; }
.zoom-wrap { overflow: hidden; display: grid; place-items: center; background: #000; min-height: 60vh; }
.zoom-wrap img { transition: transform .25s ease; }
.zoom-wrap img:hover { transform: scale(1.01); }
.modal-photo { width: auto !important; max-width: 100%; height: auto; max-height: calc(100vh - 220px); object-fit: contain; }
.caption { background: rgba(0,0,0,.55); border-top: 1px solid rgba(255,255,255,.08); font-weight: 600; letter-spacing: .3px; }
.ratio-9x16 { --bs-aspect-ratio: calc(4 / 3 * 100%); }
.card-meta { display:none; }
.pill { display:none; }
.muted { color:#6c757d; font-size:12px; }
</style>


