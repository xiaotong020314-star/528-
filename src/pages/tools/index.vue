<template>
  <view class="page">
    <!-- Header -->
    <view class="header">
      <view class="header-inner">
        <view class="header-left">
          <view class="avatar">
            <image
              class="avatar-img"
              src="https://lh3.googleusercontent.com/aida-public/AB6AXuDrwp-Ht6bWAEVcRsrBelvteAhWVQxmsDgVw4Sq7IlGS5hNakSXat0ceaf8OcCtYsOZEbQVm9U6F7vvtYvKY3OqR6JdATZR3bk-Wm8JBWQJqx6qE1WcUf4ttoXp_7yQIc55xyzKg3Q0rH9DmWoQGYEvYJf4jdfRInQO2xWtYtXY5XUgqPm5Go3Rl1clVo4wQwYw1BorbTEyMsW3d73gX0rZsA_7hNAva4IzAjH8Vzcd3rC4SfabIvRZVeSV_qRfcIc1ygJ3k4z5bEQ"
              mode="aspectFill"
            />
          </view>
          <text class="header-title">OpenClaw</text>
        </view>
        <view class="header-btn" @tap="onNotification">
          <text class="icon-font">notifications</text>
        </view>
      </view>
    </view>

    <view class="main-content">
      <!-- Task Center -->
      <view class="task-section">
        <view class="section-header">
          <text class="section-title">活动中</text>
          <text class="task-count">3 个任务</text>
        </view>
        <view class="task-list">
          <!-- Task 1: 推荐晚餐 -->
          <view class="task-item">
            <view class="task-info">
              <text class="task-name">正在为您推荐晚餐</text>
              <text class="task-percent task-percent-primary">65%</text>
            </view>
            <view class="progress-track">
              <view class="progress-fill progress-fill-primary" :style="{ width: '65%' }" />
            </view>
          </view>
          <!-- Task 2: 保洁预约 -->
          <view class="task-item">
            <view class="task-info">
              <text class="task-name">保洁预约</text>
              <text class="task-percent task-percent-secondary">100%</text>
            </view>
            <view class="progress-track">
              <view class="progress-fill progress-fill-secondary" :style="{ width: '100%' }" />
            </view>
          </view>
          <!-- Task 3: 同步体检结果 -->
          <view class="task-item">
            <view class="task-info">
              <text class="task-name">同步体检结果</text>
              <text class="task-percent task-percent-tertiary">30%</text>
            </view>
            <view class="progress-track">
              <view class="progress-fill progress-fill-tertiary" :style="{ width: '30%' }" />
            </view>
          </view>
        </view>
      </view>

      <!-- Search -->
      <view class="search-wrap">
        <view class="search-box">
          <text class="icon-font search-icon">search</text>
          <input
            class="search-input"
            type="text"
            placeholder="搜索技能..."
            placeholder-class="search-placeholder"
            :value="searchText"
            @input="onSearchInput"
          />
        </view>
      </view>

      <!-- Skill Categories & List -->
      <view class="skill-section">
        <scroll-view class="tab-scroll" scroll-x :show-scrollbar="false">
          <view class="tab-list">
            <view
              v-for="(tab, idx) in tabs"
              :key="idx"
              class="tab-item"
              :class="{ 'tab-active': activeTab === idx }"
              @tap="activeTab = idx"
            >
              <text class="tab-text" :class="{ 'tab-text-active': activeTab === idx }">{{ tab }}</text>
            </view>
          </view>
        </scroll-view>
        <view class="skill-list">
          <view
            v-for="(skill, idx) in filteredSkills"
            :key="idx"
            class="skill-item"
            @tap="onSkillTap(skill)"
          >
            <view class="skill-icon" :class="skill.iconBg">
              <text class="icon-font skill-icon-text" :class="skill.iconColor">{{ skill.icon }}</text>
            </view>
            <view class="skill-content">
              <view class="skill-header">
                <text class="skill-name">{{ skill.name }}</text>
                <text class="skill-badge" :class="skill.badgeClass">{{ skill.badge }}</text>
              </view>
              <text class="skill-desc">{{ skill.desc }}</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- Bottom Nav Bar (purely visual) -->
    <view class="bottom-nav">
      <view class="nav-item">
        <text class="icon-font nav-icon">smart_toy</text>
        <text class="nav-label">管家</text>
      </view>
      <view class="nav-item">
        <text class="icon-font nav-icon">shopping_bag</text>
        <text class="nav-label">商城</text>
      </view>
      <view class="nav-item nav-item-active">
        <text class="icon-font nav-icon-active">construction</text>
        <text class="nav-label nav-label-active">工具</text>
      </view>
      <view class="nav-item">
        <text class="icon-font nav-icon">person</text>
        <text class="nav-label">我的</text>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref, computed } from 'vue'

const statusBarHeight = ref(0)
try {
  const sysInfo = uni.getSystemInfoSync()
  statusBarHeight.value = sysInfo.statusBarHeight || 0
} catch (e) {
  statusBarHeight.value = 0
}

const searchText = ref('')
const activeTab = ref(0)

const tabs = ['全部', '生活', '健康', '工作', '家居']

const skills = [
  {
    name: '智能点餐',
    desc: '根据营养需求和预算自动选餐下单',
    icon: 'restaurant',
    iconBg: 'bg-orange',
    iconColor: 'text-orange',
    badge: '运行中',
    badgeClass: 'badge-primary',
    category: '生活',
  },
  {
    name: '智能出行',
    desc: '自动安排机票酒店，实时规避延误',
    icon: 'flight_takeoff',
    iconBg: 'bg-blue',
    iconColor: 'text-blue',
    badge: '暂停',
    badgeClass: 'badge-gray',
    category: '生活',
  },
  {
    name: '健康追踪',
    desc: '同步穿戴设备，提供主动健康提醒',
    icon: 'favorite',
    iconBg: 'bg-pink',
    iconColor: 'text-pink',
    badge: '监测中',
    badgeClass: 'badge-primary',
    category: '健康',
  },
  {
    name: '日程同步',
    desc: '跨平台日程优化，自动冲突处理',
    icon: 'event_note',
    iconBg: 'bg-indigo',
    iconColor: 'text-indigo',
    badge: '已优化',
    badgeClass: 'badge-primary',
    category: '工作',
  },
  {
    name: '预算管家',
    desc: '自动账单分类与储蓄计划执行',
    icon: 'payments',
    iconBg: 'bg-emerald',
    iconColor: 'text-emerald',
    badge: '节省 240 元',
    badgeClass: 'badge-primary',
    category: '工作',
  },
  {
    name: '家居安防',
    desc: '智能门锁与能耗监测',
    icon: 'house',
    iconBg: 'bg-amber',
    iconColor: 'text-amber',
    badge: '撤防',
    badgeClass: 'badge-gray',
    category: '家居',
  },
]

const filteredSkills = computed(() => {
  if (activeTab.value === 0) return skills
  const category = tabs[activeTab.value]
  return skills.filter((s) => s.category === category)
})

function onSearchInput(e) {
  searchText.value = e.detail.value
}

function onNotification() {
  // placeholder
}

function onSkillTap(skill) {
  // placeholder
}
</script>

<style lang="scss" scoped>
/* ===== Design Tokens ===== */
$primary: #0061a4;
$primary-container: #2f9bf7;
$secondary: #00687a;
$tertiary: #494bd6;
$on-surface: #191c1e;
$on-surface-variant: #404752;
$outline: #707883;
$surface: #f7f9fb;
$surface-container: #eceef0;
$surface-container-low: #f2f4f6;
$surface-container-high: #e6e8ea;
$outline-variant: #bfc7d4;
$white: #ffffff;

/* ===== Page ===== */
.page {
  min-height: 100vh;
  background-color: $surface-container-low;
  padding-bottom: 180rpx;
  font-size: 16px;
  color: $on-surface;
}

/* ===== Icon Font (Material Symbols) ===== */
.icon-font {
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
}

/* ===== Header ===== */
.header {
  position: sticky;
  top: 0;
  z-index: 60;
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  border-bottom: 1rpx solid $white;
}

.header-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 0 40rpx;
  height: 128rpx;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 24rpx;
}

.avatar {
  width: 64rpx;
  height: 64rpx;
  border-radius: 50%;
  overflow: hidden;
  background-color: $primary;
}

.avatar-img {
  width: 100%;
  height: 100%;
}

.header-title {
  font-size: 20px;
  font-weight: 600;
  color: $on-surface;
  letter-spacing: -0.02em;
}

.header-btn {
  width: 80rpx;
  height: 80rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  color: $on-surface-variant;
}

/* ===== Main Content ===== */
.main-content {
  padding: 48rpx 40rpx 0;
}

/* ===== Task Center ===== */
.task-section {
  margin-bottom: 64rpx;
  background-color: $white;
  padding: 48rpx;
  border-radius: 24rpx;
  box-shadow: 0px 8rpx 40rpx rgba(0, 0, 0, 0.05);
  border: 1rpx solid $white;
}

.section-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 48rpx;
}

.section-title {
  font-size: 20px;
  font-weight: 600;
  color: $on-surface;
}

.task-count {
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.02em;
  color: $outline;
  background-color: $surface-container;
  padding: 4rpx 16rpx;
  border-radius: 9999rpx;
}

.task-list {
  display: flex;
  flex-direction: column;
  gap: 48rpx;
}

.task-item {
  /* container */
}

.task-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8rpx;
}

.task-name {
  font-size: 14px;
  font-weight: 600;
  color: $on-surface;
}

.task-percent {
  font-size: 12px;
  font-weight: 700;

  &-primary {
    color: $primary;
  }

  &-secondary {
    color: $secondary;
  }

  &-tertiary {
    color: $tertiary;
  }
}

.progress-track {
  width: 100%;
  background-color: $surface-container-high;
  height: 20rpx;
  border-radius: 9999rpx;
  overflow: hidden;
  box-shadow: inset 0 1rpx 2rpx rgba(0, 0, 0, 0.06);
}

.progress-fill {
  height: 100%;
  border-radius: 9999rpx;
  transition: width 0.5s ease;

  &-primary {
    background-color: $primary;
    box-shadow: 0 0 16rpx rgba(0, 97, 164, 0.4);
  }

  &-secondary {
    background-color: $secondary;
    box-shadow: 0 0 16rpx rgba(0, 104, 122, 0.4);
  }

  &-tertiary {
    background-color: $tertiary;
    box-shadow: 0 0 16rpx rgba(73, 75, 214, 0.4);
  }
}

/* ===== Search ===== */
.search-wrap {
  margin-bottom: 64rpx;
}

.search-box {
  position: relative;
  background-color: $white;
  border-radius: 24rpx;
  box-shadow: 0px 8rpx 40rpx rgba(0, 0, 0, 0.05);
  border: 1rpx solid $white;
  display: flex;
  align-items: center;
  padding: 0 32rpx;
}

.search-icon {
  color: $primary;
  margin-right: 16rpx;
}

.search-input {
  flex: 1;
  border: none;
  padding: 32rpx 0;
  font-size: 16px;
  background-color: transparent;
  color: $on-surface;
}

.search-placeholder {
  color: rgba(112, 120, 131, 0.6);
}

/* ===== Skill Section ===== */
.skill-section {
  background-color: $white;
  border-radius: 24rpx;
  box-shadow: 0px 8rpx 40rpx rgba(0, 0, 0, 0.05);
  border: 1rpx solid $white;
  padding: 48rpx;
}

.tab-scroll {
  white-space: nowrap;
  margin-bottom: 0;
}

.tab-list {
  display: flex;
  gap: 48rpx;
  padding-bottom: 24rpx;
  border-bottom: 1rpx solid $surface-container;
  margin-bottom: 48rpx;
}

.tab-item {
  flex-shrink: 0;
  padding-bottom: 24rpx;
  border-bottom: 4rpx solid transparent;
}

.tab-active {
  border-bottom-color: $primary;
}

.tab-text {
  font-size: 14px;
  font-weight: 500;
  letter-spacing: 0.01em;
  color: $on-surface-variant;
  white-space: nowrap;
}

.tab-text-active {
  font-weight: 700;
  color: $primary;
}

/* ===== Skill List ===== */
.skill-list {
  display: flex;
  flex-direction: column;
  gap: 16rpx;
}

.skill-item {
  display: flex;
  align-items: center;
  gap: 32rpx;
  padding: 24rpx;
  border-radius: 24rpx;
  border: 1rpx solid transparent;
}

.skill-icon {
  width: 96rpx;
  height: 96rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 24rpx;
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.04);
  flex-shrink: 0;

  .skill-icon-text {
    font-size: 24px;
  }
}

.bg-orange {
  background-color: #fff7ed;
}
.text-orange {
  color: #f97316;
}
.bg-blue {
  background-color: #eff6ff;
}
.text-blue {
  color: #3b82f6;
}
.bg-pink {
  background-color: #fdf2f8;
}
.text-pink {
  color: #ec4899;
}
.bg-indigo {
  background-color: #eef2ff;
}
.text-indigo {
  color: #6366f1;
}
.bg-emerald {
  background-color: #ecfdf5;
}
.text-emerald {
  color: #10b981;
}
.bg-amber {
  background-color: #fffbeb;
}
.text-amber {
  color: #f59e0b;
}

.skill-content {
  flex-grow: 1;
  min-width: 0;
}

.skill-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skill-name {
  font-size: 14px;
  font-weight: 700;
  color: $on-surface;
}

.skill-badge {
  font-size: 10px;
  font-weight: 700;
  padding: 2rpx 16rpx;
  border-radius: 8rpx;
}

.badge-primary {
  background-color: rgba(47, 155, 247, 0.2);
  color: $primary;
}

.badge-gray {
  background-color: $surface-container;
  color: $outline;
}

.skill-desc {
  font-size: 13px;
  color: $on-surface-variant;
  margin-top: 4rpx;
  lines: 1;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
}

/* ===== Bottom Nav ===== */
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
  padding-left: 32rpx;
  padding-right: 32rpx;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  border-top: 1rpx solid $white;
  box-shadow: 0 -8rpx 48rpx rgba(0, 0, 0, 0.04);
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 8rpx 32rpx;
  color: rgba(64, 71, 82, 0.4);

  .nav-icon {
    font-size: 24px;
  }

  .nav-label {
    font-size: 10px;
    font-weight: 500;
    letter-spacing: 0.02em;
  }
}

.nav-item-active {
  color: $primary;

  .nav-icon-active {
    font-size: 24px;
    font-variation-settings: 'FILL' 1;
  }

  .nav-label-active {
    font-size: 10px;
    font-weight: 700;
  }
}
</style>
