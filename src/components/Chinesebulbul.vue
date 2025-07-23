<template>
  <div class="container-fluid">
    <div class="row flex-lg-nowrap g-0">

      <!-- Mobile 漢堡按鈕 -->
      <div class="mobile-header d-lg-none p-2  py-3 w-100 d-flex justify-content-between align-items-center">
        <button class="btn btn-outline-secondary" @click="toggleSidebar">
          <i :class="sidebarVisible ? 'bi bi-x-lg' : 'bi bi-list'"></i> 
        </button>
        <h5 class="mb-0 flex-grow-1 text-center">白頭翁不吃小米</h5>

        <!-- Logo -->
        <div class="logo-wrapper-mobile">
          <div class="logo">
            <div class="bird">
              <div class="face"></div>
              <div class="eye"></div>
              <div class="beak"></div>
            </div>
          </div>
        </div>
      </div>

      <!-- Sidebar -->
      <div
        class="sidebar p-5 col-12 col-lg-auto"
        :class="{ 'd-none': !sidebarVisible && isMobile }"
      >
         <div class="bulbul">
          <h4 class="sidebar-title">白頭翁不吃小米</h4>
          <div class="logo-wrapper">
            <div class="logo">
              <div class="bird">
                <div class="face"></div>
                <div class="eye"></div>
                <div class="beak"></div>
              </div>
            </div>
          </div>
        </div>

        <ul class="nav flex-column text-center">
          <li class="nav-item" v-for="item in menuItems":key="item.id">
            <a class="nav-link" :class="{ selected: selectedItem === item.id }"
               @click.prevent="selectItem(item.id)">
              {{ item.label }}
            </a>
          </li>
      </ul>
     </div>

      <div class="col">
        <div class="banner">
          <div class="banner-text">
            <h2>白頭翁 (Chinese bulbul)</h2>
            <p>又名白頭鵯。以果實、昆蟲為主食，無法消化小米、穀類。平均壽命約 8~10 年。</p>
          </div>
        </div>
        <div class="feature row w-100 m-0">
          <div
            class="col-12 col-md-4 p-4 d-flex align-items-center feature-box"
            v-for="item in features"
            :key="item.id"
          >
            <div class="feature-title">{{ item.title }}</div>
            <p class="feature-content">{{ item.content }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sidebarVisible = ref(false)
const isMobile = ref(false)

const checkViewport = () => {
  isMobile.value = window.innerWidth < 992
  if (!isMobile.value) sidebarVisible.value = true
  else sidebarVisible.value = false
}

const toggleSidebar = () => {
  sidebarVisible.value = !sidebarVisible.value
}

onMounted(() => {
  checkViewport()
  window.addEventListener('resize', checkViewport)
})

const selectedItem = ref('feature') 
const menuItems = [
  { id: 'feature', label: '白頭翁的特性' },
  { id: 'story', label: '白頭翁的故事' },
  { id: 'photo', label: '白頭翁的美照' },
  { id: 'crisis', label: '白頭翁的危機' },
]

const selectItem = (id) => {
  selectedItem.value = id
}

const features = [
  {
    id: 1,
    title: '外觀',
    content: '白頭鵯體長約17到22公分，額至頭頂純黑色而富有光澤，兩眼上方至後枕白色，形成一白色枕環。耳羽後部有一白斑，此白環與白斑在黑色的頭部均極為醒目，老鳥的枕羽(後頭部)更潔白，所以又叫「白頭翁」。'
  },
  {
    id: 2,
    title: '棲地',
    content: '白頭翁和麻雀、綠繡眼合稱「城市三寶」，常成群出現在平原區灌木叢、丘陵樹林地帶，以及校園、公園、庭院、行道中的各種高高的電線與樹上。'
  },
  {
    id: 3,
    title: '食性',
    content: '以果樹的漿果和種子為主食，並時常飛入果園偷吃果實，還會吃嫩葉嫩芽，尤其是胡蝶蘭的嫩葉嫩芽葉，偶爾啄食昆蟲。'
  }
]
</script>
