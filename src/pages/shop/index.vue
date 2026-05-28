<template>
  <view class="page">
    <!-- Header -->
    <view class="header" :class="{ 'header--bordered': isHeaderBordered }">
      <view class="header__left">
        <view class="avatar">
          <image
            class="avatar__img"
            src="https://lh3.googleusercontent.com/aida-public/AB6AXuDOYoQUN1LsRRKZkAU49uXh0w4ZbfbY_rsdfyXt6stWVw1qMyppXZrFFUsv_5BeMCkfW4uGzIjcMSN1XQ7NoUNahtphErnNQyP-D2qqXTnT9RqYNuuZvDW2Yv_yPLIJqCSPycdEcT4_2TaSuGsEbGYXt2VCPfYeTJILx5k2Zjn_XIlKmwFKE9FmwAscYhGP8RYjm6fcaAtZPokh3cSHSuKeTh_pGdAXJn-eqvX_0wLcqLh_43PSj-zsPv-XD6qle8x5EZIix_c4Xe8"
            mode="aspectFill"
          />
        </view>
        <text class="header__title">OpenClaw</text>
      </view>
      <view class="header__right">
        <view class="icon-btn" @tap="onNotification">
          <text class="icon icon--xl">notifications</text>
        </view>
      </view>
    </view>

    <!-- Main Content -->
    <view class="main">
      <!-- Search Bar -->
      <view class="search-section">
        <view class="search-bar">
          <view class="search-bar__icon">
            <text class="icon icon--sm">search</text>
          </view>
          <input
            class="search-bar__input"
            placeholder="想吃点什么？"
            placeholder-class="search-bar__placeholder"
            confirm-type="search"
          />
        </view>
      </view>

      <!-- Category Icon Grid 4x2 -->
      <view class="category-grid">
        <view
          v-for="item in categories"
          :key="item.label"
          class="category-item"
          @tap="onCategoryTap(item)"
        >
          <view class="category-item__icon-wrap">
            <text class="icon icon--2xl">{{ item.icon }}</text>
          </view>
          <text class="category-item__label">{{ item.label }}</text>
        </view>
      </view>

      <!-- Tabs -->
      <view class="tabs-section">
        <scroll-view scroll-x class="tabs-scroll" :show-scrollbar="false">
          <view class="tabs">
            <view
              v-for="(tab, idx) in tabs"
              :key="tab"
              class="tab-item"
              :class="{ 'tab-item--active': activeTab === idx }"
              @tap="activeTab = idx"
            >
              <text class="tab-item__text" :class="{ 'tab-item__text--active': activeTab === idx }">{{ tab }}</text>
              <view v-if="activeTab === idx" class="tab-item__indicator" />
            </view>
          </view>
        </scroll-view>
      </view>

      <!-- AI Curated Section -->
      <view class="curated-section">
        <view class="curated-header">
          <text class="curated-header__title">AI 精选</text>
          <text class="curated-header__link" @tap="onViewAll">查看全部</text>
        </view>
        <view class="curated-list">
          <view
            v-for="card in aiCards"
            :key="card.name"
            class="shop-card"
            @tap="onShopCardTap(card)"
          >
            <view class="shop-card__img-wrap">
              <image class="shop-card__img" :src="card.image" mode="aspectFill" />
              <view class="shop-card__match">
                <text class="shop-card__match-text">{{ card.match }}% Match</text>
              </view>
            </view>
            <view class="shop-card__info">
              <view class="shop-card__left">
                <text class="shop-card__name">{{ card.name }}</text>
                <view class="shop-card__tags">
                  <text class="shop-card__tag-text">{{ card.tags }}</text>
                  <view class="shop-card__dot" />
                  <text class="shop-card__distance">{{ card.distance }}</text>
                </view>
              </view>
              <view class="shop-card__right">
                <view class="shop-card__rating">
                  <text class="icon icon--star">star</text>
                  <text class="shop-card__rating-num">{{ card.rating }}</text>
                </view>
                <text class="shop-card__price">{{ card.price }} avg</text>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- Bottom Nav Bar (visual only) -->
    <view class="bottom-nav">
      <view
        v-for="nav in bottomNavItems"
        :key="nav.label"
        class="bottom-nav__item"
        :class="{ 'bottom-nav__item--active': nav.active }"
      >
        <text
          class="icon icon--nav"
          :class="{ 'icon--nav-active': nav.active }"
        >{{ nav.icon }}</text>
        <text
          class="bottom-nav__label"
          :class="{ 'bottom-nav__label--active': nav.active }"
        >{{ nav.label }}</text>
      </view>
    </view>

    <!-- AI Toast (visual only) -->
    <view class="ai-toast" :class="{ 'ai-toast--visible': showToast }">
      <view class="ai-toast__content">
        <view class="ai-toast__icon-wrap">
          <text class="icon icon--toast">auto_awesome</text>
        </view>
        <view class="ai-toast__text-wrap">
          <text class="ai-toast__text">需要为您预订 45 分钟后的喜茶吗？</text>
        </view>
        <view class="ai-toast__action" @tap="showToast = false">
          <text class="ai-toast__action-text">好</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const statusBarHeight = ref(0)
const isHeaderBordered = ref(false)
const activeTab = ref(0)
const showToast = ref(false)

const categories = [
  { icon: 'restaurant', label: '外卖' },
  { icon: 'eco', label: '生鲜' },
  { icon: 'store', label: '便利店' },
  { icon: 'chair', label: '到店' },
  { icon: 'local_taxi', label: '打车' },
  { icon: 'cleaning_services', label: '家政' },
  { icon: 'health_and_safety', label: '健康' },
  { icon: 'more_horiz', label: '更多' },
]

const tabs = ['推荐', '外卖', '到店吃', '生鲜', '健康餐']

const aiCards = [
  {
    name: '青禾轻食',
    tags: '低脂 • 高蛋白 • 无花生',
    distance: '2.4km',
    rating: '4.9',
    price: '$22',
    match: '98',
    image: 'https://lh3.googleusercontent.com/aida-public/AB6AXuBUY0CW7vaoL8LSMZ1bUXyologsvlyj6aTUgEpIi4WOI2jiu_iGiF7nqpyC_mFcMurSzNv041--F8RqDrreeu53Yb5KgtH_PakaFLOXVfx6GSnE4BU9buOOu8_LDUiCHqemM190ObPNL5dYzNrXqotdXpsQXcsMp5A8tvZM-qVviHtR1qnatsnBtoLpol3M11Y88T2UjSZVK1rc8euS_7HTwOEMEoQhKXmso8SKpwRRAm1KkcsG9NJkSf9JRLswGJK4j46VT89vc6o',
  },
  {
    name: '老街面馆',
    tags: '传统面食 • 出餐快',
    distance: '1.1km',
    rating: '4.7',
    price: '$15',
    match: '92',
    image: 'https://lh3.googleusercontent.com/aida-public/AB6AXuDUGJoZHWAUyb8NErzW7gNMoMMTZUd5Eonii2ir6dm7QK-gWsOPtXXfk8ac7-hd8JvojBm456FfIXRtJe9qfRIAMAe5jgwG73FEFGIJDC0UZ8NcsMc4Kh3Jaun8r52S7a5SCYMXGOUWbe7f2MM7qYWZ3bFi41Xr3jkb5SWIb_Uq3SHqsdyGMjEFNN3DT8CgG3h1a8crjkciKKsGCAREZBhXF_f0oqbYzMt0VQgFYKjfpF-U3uSpoOoj-23Iq9sQ6whhToFkpzVjQBM',
  },
  {
    name: '喜茶 GO',
    tags: '低糖可选 • 人气爆款',
    distance: '0.5km',
    rating: '4.8',
    price: '$8',
    match: '88',
    image: 'https://lh3.googleusercontent.com/aida-public/AB6AXuBVH89TlcSVId11h_bMfud1V4z7usZNQ97CygHJffXa5kY4ICSRY7SnXeVqxmQG14rnjQ5oJdNGDkZW-0Kz4RtTnP4eiST-5_RqXHf1fW8xLPXYvvk5wu7iqhR-5XdA_lFjm-1tLQGDRG5uvr8b3k5t3DmIDhYWYOvbwvRTlFCihsOe4NIw2JsWYAceRurPFbqK_SM_hQXywa7J7ITvc_EYEf3ZznyMAKU-XSt8YY3n16xeHCctymEhG5sSoMdXCQ-Zi_VovhTTsdw',
  },
]

const bottomNavItems = [
  { icon: 'smart_toy', label: '管家', active: false },
  { icon: 'shopping_bag', label: '商城', active: true },
  { icon: 'apps', label: '服务', active: false },
  { icon: 'person', label: '我的', active: false },
]

onMounted(() => {
  const sysInfo = uni.getSystemInfoSync()
  statusBarHeight.value = sysInfo.statusBarHeight || 0

  setTimeout(() => {
    showToast.value = true
  }, 2000)
})

function onNotification() {}
function onCategoryTap() {}
function onViewAll() {}
function onShopCardTap() {}

// Scroll handler for header border
function onPageScroll(e) {
  isHeaderBordered.value = e.scrollTop > 10
}

defineExpose({ onPageScroll })
</script>

<style lang="scss" scoped>
/* ===== Design Tokens ===== */
$bg: #ffffff;
$surface: #f7f9fb;
$surface-container-low: #ffffff;
$surface-container: #eceef0;
$surface-container-lowest: #ffffff;
$on-surface: #191c1e;
$on-surface-variant: #404752;
$primary: #0061a4;
$primary-container: #2f9bf7;
$outline-variant: #bfc7d4;
$yellow-500: #eab308;

/* ===== Page ===== */
.page {
  min-height: 100vh;
  background-color: $bg;
  color: $on-surface;
  font-family: 'Hanken Grotesk', 'Geist', sans-serif;
  font-size: 16px;
  line-height: 24px;
  padding-bottom: 200rpx;
}

/* ===== Icon (Remixicon-compatible text placeholder) ===== */
.icon {
  font-family: 'Material Symbols Outlined';
  font-size: 24px;
  font-style: normal;
  font-weight: normal;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
  -webkit-font-smoothing: antialiased;

  &--sm { font-size: 20px; }
  &--xl { font-size: 20px; }
  &--2xl { font-size: 28px; }
  &--nav { font-size: 24px; }
  &--nav-active { font-size: 24px; }
  &--star {
    font-size: 14px;
    color: $yellow-500;
    font-variation-settings: 'FILL' 1;
  }
  &--toast { font-size: 20px; color: #fff; }
}

/* ===== Header ===== */
.header {
  position: sticky;
  top: 0;
  z-index: 50;
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 0 48rpx;
  height: 128rpx;
  background-color: rgba($bg, 0.95);
  transition: all 0.3s;

  &--bordered {
    border-bottom: 2rpx solid $surface-container-low;
  }

  &__left {
    display: flex;
    align-items: center;
    gap: 24rpx;
  }

  &__right {
    display: flex;
    align-items: center;
    gap: 32rpx;
  }

  &__title {
    font-size: 18px;
    font-weight: 700;
    letter-spacing: -0.01em;
    color: $on-surface;
  }
}

.avatar {
  width: 64rpx;
  height: 64rpx;
  border-radius: 50%;
  overflow: hidden;

  &__img {
    width: 100%;
    height: 100%;
  }
}

.icon-btn {
  color: $on-surface;
  transition: opacity 0.2s;

  &:active {
    opacity: 0.6;
  }
}

/* ===== Search Bar ===== */
.search-section {
  padding: 0 48rpx;
  margin-top: 16rpx;
}

.search-bar {
  position: relative;
  display: flex;
  align-items: center;

  &__icon {
    position: absolute;
    left: 32rpx;
    color: rgba($on-surface-variant, 0.4);
  }

  &__input {
    width: 100%;
    height: 88rpx;
    padding-left: 88rpx;
    padding-right: 32rpx;
    border-radius: 9999rpx;
    border: none;
    background-color: $surface-container-low;
    font-size: 14px;
    color: $on-surface;
    transition: background-color 0.2s;
  }

  &__placeholder {
    color: rgba($on-surface-variant, 0.5);
    font-size: 14px;
  }
}

/* ===== Category Grid ===== */
.category-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  row-gap: 64rpx;
  padding: 0 48rpx;
  margin-top: 80rpx;
}

.category-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 16rpx;
  -webkit-tap-highlight-color: transparent;

  &__icon-wrap {
    width: 80rpx;
    height: 80rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    color: $on-surface-variant;
    transition: transform 0.15s;

    &:active {
      transform: scale(0.9);
    }
  }

  &__label {
    font-size: 11px;
    font-weight: 500;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    color: rgba($on-surface-variant, 0.8);
  }
}

/* ===== Tabs ===== */
.tabs-section {
  margin-top: 80rpx;
}

.tabs-scroll {
  white-space: nowrap;
}

.tabs {
  display: flex;
  gap: 64rpx;
  padding: 0 48rpx 32rpx;
  border-bottom: 2rpx solid $surface-container-low;
}

.tab-item {
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-bottom: 16rpx;

  &__text {
    font-size: 14px;
    font-weight: 500;
    letter-spacing: 0.01em;
    color: $on-surface-variant;

    &--active {
      color: $on-surface;
    }
  }

  &__indicator {
    width: 100%;
    height: 4rpx;
    background-color: $primary;
    border-radius: 2rpx;
    margin-top: 8rpx;
  }
}

/* ===== AI Curated Section ===== */
.curated-section {
  margin-top: 80rpx;
  padding: 0 48rpx;
}

.curated-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 64rpx;

  &__title {
    font-size: 20px;
    font-weight: 500;
    letter-spacing: -0.01em;
  }

  &__link {
    font-size: 12px;
    color: $on-surface-variant;
    text-decoration: underline;
    text-underline-offset: 8rpx;
  }
}

.curated-list {
  display: flex;
  flex-direction: column;
  gap: 80rpx;
}

/* ===== Shop Card ===== */
.shop-card {
  -webkit-tap-highlight-color: transparent;

  &__img-wrap {
    position: relative;
    width: 100%;
    aspect-ratio: 16 / 9;
    border-radius: 32rpx;
    overflow: hidden;
    background-color: $surface-container-low;
    margin-bottom: 32rpx;
  }

  &__img {
    width: 100%;
    height: 100%;
  }

  &__match {
    position: absolute;
    top: 32rpx;
    left: 32rpx;
    background-color: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(12px);
    -webkit-backdrop-filter: blur(12px);
    padding: 8rpx 16rpx;
    border-radius: 8rpx;
  }

  &__match-text {
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: $on-surface;
  }

  &__info {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }

  &__left {
    display: flex;
    flex-direction: column;
    gap: 8rpx;
  }

  &__name {
    font-size: 18px;
    font-weight: 600;
  }

  &__tags {
    display: flex;
    align-items: center;
    gap: 16rpx;
  }

  &__tag-text {
    font-size: 12px;
    color: $on-surface-variant;
  }

  &__dot {
    width: 8rpx;
    height: 8rpx;
    border-radius: 50%;
    background-color: $outline-variant;
  }

  &__distance {
    font-size: 12px;
    color: $on-surface-variant;
  }

  &__right {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
  }

  &__rating {
    display: flex;
    align-items: center;
    gap: 8rpx;
  }

  &__rating-num {
    font-size: 12px;
    font-weight: 700;
  }

  &__price {
    font-size: 12px;
    color: $on-surface-variant;
    margin-top: 4rpx;
  }
}

/* ===== Bottom Nav (visual only) ===== */
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  z-index: 50;
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding-top: 24rpx;
  padding-bottom: 64rpx;
  padding-left: 64rpx;
  padding-right: 64rpx;
  background-color: rgba($bg, 0.8);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-top: 2rpx solid $surface-container-low;

  &__item {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: $on-surface-variant;
    transition: color 0.2s;

    &--active {
      color: $primary;
    }
  }

  &__label {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.02em;
    margin-top: 8rpx;
    color: $on-surface-variant;

    &--active {
      color: $primary;
    }
  }
}

/* ===== AI Toast (visual only) ===== */
.ai-toast {
  position: fixed;
  bottom: 192rpx;
  left: 50%;
  transform: translateX(-50%) translateY(32rpx);
  z-index: 50;
  width: 88%;
  max-width: 750rpx;
  opacity: 0;
  transition: all 0.7s;

  &--visible {
    opacity: 1;
    transform: translateX(-50%) translateY(0);
  }

  &__content {
    background-color: $on-surface;
    color: $surface;
    padding: 32rpx;
    border-radius: 32rpx;
    display: flex;
    align-items: center;
    gap: 32rpx;
    box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.15);
  }

  &__icon-wrap {
    background-color: $primary;
    padding: 16rpx;
    border-radius: 50%;
    flex-shrink: 0;
  }

  &__text-wrap {
    flex: 1;
  }

  &__text {
    font-size: 12px;
    line-height: 1.5;
    opacity: 0.9;
    color: $surface;
  }

  &__action {
    font-size: 12px;
    font-weight: 700;
    padding: 16rpx 24rpx;
    background-color: $primary;
    color: #fff;
    border-radius: 16rpx;
    flex-shrink: 0;
  }

  &__action-text {
    font-size: 12px;
    font-weight: 700;
    color: #fff;
  }
}
</style>
