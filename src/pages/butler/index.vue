<template>
  <view class="butler-page">
    <!-- Status Bar Spacer -->
    <view :style="{ height: statusBarHeight + 'px' }"></view>

    <!-- Header -->
    <view class="header fade-in-section" :style="{ animationDelay: '0s' }">
      <view class="header-left">
        <view class="avatar"></view>
        <text class="brand-title">OpenClaw</text>
      </view>
      <view class="header-right">
        <view class="notification-btn">
          <text class="material-symbols-outlined icon-24">notifications</text>
          <view class="notification-dot"></view>
        </view>
      </view>
    </view>

    <!-- Main Content -->
    <view class="main-content">
      <!-- Hero Interaction Zone -->
      <view class="hero-section fade-in-section" :style="{ animationDelay: '0.05s' }">
        <view class="hero-deco-1"></view>
        <view class="hero-deco-2"></view>
        <view class="hero-content">
          <!-- AI Orb + Welcome -->
          <view class="ai-orb-row">
            <view class="ai-orb">
              <view class="ai-ring"></view>
              <view class="ai-ring ai-ring-2"></view>
              <view class="ai-ring ai-ring-3"></view>
            </view>
            <view class="welcome-text">
              <text class="welcome-title">早安，主人</text>
              <text class="welcome-subtitle">今天我会全程为您打理</text>
            </view>
          </view>
          <!-- Input Area -->
          <view class="input-area">
            <view class="input-wrapper">
              <input
                class="message-input"
                type="text"
                placeholder="给管家发消息..."
                disabled
              />
              <view class="send-btn">
                <text class="material-symbols-outlined icon-20">arrow_upward</text>
              </view>
            </view>
            <view class="action-btns">
              <view class="voice-btn">
                <text class="material-symbols-outlined icon-24">mic</text>
                <text class="voice-btn-label">语音对话</text>
              </view>
              <view class="grid-btn">
                <text class="material-symbols-outlined icon-24">grid_view</text>
              </view>
            </view>
          </view>
        </view>
      </view>

      <!-- Today's Focus -->
      <view class="section-container today-section fade-in-section" :style="{ animationDelay: '0.1s' }">
        <view class="section-header">
          <text class="section-title">今日重点</text>
          <view class="suggestion-badge">
            <text class="suggestion-badge-text">3 条建议</text>
          </view>
        </view>
        <scroll-view scroll-x :show-scrollbar="false" class="cards-scroll">
          <view class="cards-row">
            <!-- Card 1: Weather -->
            <view class="focus-card focus-card--primary">
              <view class="focus-card-head">
                <text class="material-symbols-outlined icon-22 focus-icon--primary">umbrella</text>
                <text class="focus-label--primary">气象预警</text>
              </view>
              <text class="focus-card-desc">预计傍晚通勤时段有大雨，建议帮您预约下午 5:30 的专车。</text>
              <view class="focus-card-actions">
                <view class="btn-primary">
                  <text class="btn-primary-text">立即预约</text>
                </view>
                <view class="btn-secondary">
                  <text class="btn-secondary-text">稍后</text>
                </view>
              </view>
            </view>
            <!-- Card 2: Health -->
            <view class="focus-card focus-card--rose">
              <view class="focus-card-head">
                <text class="material-symbols-outlined icon-22 focus-icon--rose">favorite</text>
                <text class="focus-label--rose">家人健康</text>
              </view>
              <text class="focus-card-desc">您父亲的睡眠质量连续3天较低，建议今天抽空进行视频沟通。</text>
              <view class="focus-card-actions">
                <view class="btn-outline">
                  <text class="btn-outline-text">拨打电话</text>
                </view>
              </view>
            </view>
          </view>
        </scroll-view>
      </view>

      <!-- Scene Timeline -->
      <view class="section-container timeline-section fade-in-section" :style="{ animationDelay: '0.15s' }">
        <text class="section-title">场景日程</text>
        <view class="timeline">
          <!-- Item 1 -->
          <view class="timeline-item">
            <view class="timeline-dot">
              <text class="material-symbols-outlined icon-18">alarm</text>
            </view>
            <view class="timeline-info">
              <text class="timeline-time">07:00 AM</text>
              <text class="timeline-name">智能唤醒</text>
              <text class="timeline-desc">已在浅眠阶段温柔唤醒，窗帘自动开启</text>
            </view>
          </view>
          <!-- Item 2 -->
          <view class="timeline-item">
            <view class="timeline-dot">
              <text class="material-symbols-outlined icon-18">restaurant</text>
            </view>
            <view class="timeline-info">
              <text class="timeline-time">12:30 PM</text>
              <text class="timeline-name">营养午餐</text>
              <text class="timeline-desc">地中海沙拉配送中，预计15分钟后到达</text>
            </view>
          </view>
          <!-- Item 3 (Active) -->
          <view class="timeline-item">
            <view class="timeline-dot timeline-dot--active">
              <text class="material-symbols-outlined icon-18">directions_car</text>
            </view>
            <view class="timeline-active-card glass-card">
              <view class="timeline-active-header">
                <text class="timeline-active-time">05:30 PM (预计)</text>
                <view class="pulse-dot"></view>
              </view>
              <text class="timeline-active-name">下班通勤规划</text>
              <text class="timeline-active-desc">已规划避堵路线，您的特斯拉已开启哨兵模式</text>
            </view>
          </view>
        </view>
      </view>

      <!-- Smart Services -->
      <view class="section-container services-section fade-in-section" :style="{ animationDelay: '0.2s' }">
        <text class="section-title">智能服务</text>
        <view class="services-grid">
          <view class="service-card">
            <view class="service-icon service-icon--orange">
              <text class="material-symbols-outlined icon-24">restaurant</text>
            </view>
            <text class="service-name">健康餐饮</text>
          </view>
          <view class="service-card">
            <view class="service-icon service-icon--blue">
              <text class="material-symbols-outlined icon-24">electric_car</text>
            </view>
            <text class="service-name">智慧出行</text>
          </view>
          <view class="service-card">
            <view class="service-icon service-icon--green">
              <text class="material-symbols-outlined icon-24">fitness_center</text>
            </view>
            <text class="service-name">体能管理</text>
          </view>
          <view class="service-card">
            <view class="service-icon service-icon--purple">
              <text class="material-symbols-outlined icon-24">cleaning_services</text>
            </view>
            <text class="service-name">环境管家</text>
          </view>
          <view class="service-wide">
            <view class="service-wide-left">
              <view class="service-wide-icon">
                <text class="material-symbols-outlined icon-24">calendar_month</text>
              </view>
              <text class="service-wide-name">第三方日程同步</text>
            </view>
            <text class="material-symbols-outlined icon-24 service-wide-arrow">chevron_right</text>
          </view>
          <view class="service-wide service-wide--danger">
            <view class="service-wide-left">
              <view class="service-wide-icon service-wide-icon--danger">
                <text class="material-symbols-outlined icon-24">emergency</text>
              </view>
              <text class="service-wide-name service-wide-name--danger">安全与紧急预案</text>
            </view>
            <text class="material-symbols-outlined icon-24 service-wide-arrow service-wide-arrow--danger">chevron_right</text>
          </view>
        </view>
      </view>
    </view>

    <!-- Floating Action Chips -->
    <view class="floating-actions">
      <scroll-view scroll-x :show-scrollbar="false" class="chips-scroll">
        <view class="chips-row">
          <view class="chip glass-card">
            <text class="material-symbols-outlined icon-20 chip-icon">mic</text>
            <text class="chip-text">语音速记</text>
          </view>
          <view class="chip glass-card">
            <text class="material-symbols-outlined icon-20 chip-icon">edit_note</text>
            <text class="chip-text">快捷任务</text>
          </view>
        </view>
      </scroll-view>
    </view>

  </view>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const statusBarHeight = ref(0)

onMounted(() => {
  const systemInfo = uni.getSystemInfoSync()
  statusBarHeight.value = systemInfo.statusBarHeight || 0
})
</script>

<style lang="scss" scoped>
/* ===== Design Tokens ===== */
$primary: #2f9bf7;
$primary-container: #eef7ff;
$on-background: #0f172a;
$on-surface: #1e293b;
$on-surface-variant: #64748b;
$on-primary: #ffffff;
$on-primary-container: #003156;
$on-error-container: #93000a;
$error: #ef4444;
$background: #f8fafc;
$surface: #ffffff;
$surface-variant: #f8fafc;
$outline: #cbd5e1;
$outline-variant: #e2e8f0;
$secondary: #475569;
$tertiary: #6366f1;
$slate-50: #f8fafc;
$slate-100: #f1f5f9;
$slate-200: #e2e8f0;
$slate-300: #cbd5e1;
$slate-400: #94a3b8;
$rose-500: #f43f5e;
$orange-500: #f97316;
$blue-500: #3b82f6;
$green-500: #22c55e;
$purple-500: #a855f7;

/* ===== Page ===== */
.butler-page {
  min-height: 100vh;
  background: $background;
  color: $on-background;
  padding-bottom: 320rpx;
}

/* ===== Entrance Animation (uses global fadeInUp from App.vue) ===== */
.fade-in-section {
  animation: fadeInUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) both;
}

/* ===== Icon Size Helpers (font-size preserved in px) ===== */
.icon-18 { font-size: 18px; }
.icon-20 { font-size: 20px; }
.icon-22 { font-size: 22px; }
.icon-24 { font-size: 24px; }
.icon-26 { font-size: 26px; }
.icon-28 { font-size: 28px; }

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
  height: 160rpx;
  background: rgba(255, 255, 255, 0.8);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  border-bottom: 2rpx solid rgba($slate-100, 0.5);
}

.header-left {
  display: flex;
  align-items: center;
  gap: 24rpx;
}

.avatar {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  background: rgba($primary, 0.1);
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  border: 2rpx solid rgba($primary, 0.2);
}

.brand-title {
  font-size: 20px;
  line-height: 28px;
  font-weight: 600;
  letter-spacing: -0.01em;
  color: $on-background;
  font-family: 'Hanken Grotesk', sans-serif;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 16rpx;
}

.notification-btn {
  width: 80rpx;
  height: 80rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  color: $on-surface-variant;
  border-radius: 50%;
  position: relative;
  &:active {
    background: $slate-100;
  }
}

.notification-dot {
  position: absolute;
  top: 20rpx;
  right: 20rpx;
  width: 16rpx;
  height: 16rpx;
  background: $primary;
  border-radius: 50%;
  border: 4rpx solid #ffffff;
}

/* ===== Main Content ===== */
.main-content {
  padding: 0 48rpx;
  margin-top: 16rpx;

  > view + view {
    margin-top: 64rpx;
  }
}

/* ===== Hero Section ===== */
.hero-section {
  position: relative;
  overflow: hidden;
  padding: 64rpx 48rpx 80rpx;
  border-radius: 64rpx;
  background: linear-gradient(to bottom right, rgba($primary, 0.1), rgba($primary, 0.05), #ffffff);
  border: 2rpx solid rgba($primary, 0.1);
  box-shadow: 0 16rpx 60rpx rgba($primary, 0.08);
}

.hero-deco-1 {
  position: absolute;
  top: -160rpx;
  right: -160rpx;
  width: 512rpx;
  height: 512rpx;
  background: rgba($primary, 0.05);
  border-radius: 50%;
  filter: blur(128rpx);
}

.hero-deco-2 {
  position: absolute;
  bottom: -80rpx;
  left: -40rpx;
  width: 384rpx;
  height: 384rpx;
  background: rgba($secondary, 0.05);
  border-radius: 50%;
  filter: blur(80rpx);
}

.hero-content {
  position: relative;
  z-index: 10;
  display: flex;
  flex-direction: column;
  gap: 48rpx;
}

/* AI Orb */
.ai-orb-row {
  display: flex;
  align-items: center;
  gap: 40rpx;
}

.ai-orb {
  position: relative;
  width: 112rpx;
  height: 112rpx;
  background: radial-gradient(circle at 30% 30%, #4facfe 0%, #0061a4 100%);
  border-radius: 50%;
  animation: orb-pulse 4s ease-in-out infinite;
  flex-shrink: 0;
}

.ai-ring {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: 3rpx solid rgba($primary, 0.4);
  border-radius: 50%;
  animation: ring-expand 3s cubic-bezier(0.16, 1, 0.3, 1) infinite;
}

.ai-ring-2 { animation-delay: 1s; }
.ai-ring-3 { animation-delay: 2s; }

.welcome-text {
  display: flex;
  flex-direction: column;
}

.welcome-title {
  font-size: 24px;
  line-height: 32px;
  font-weight: 600;
  color: $on-background;
  font-family: 'Hanken Grotesk', sans-serif;
}

.welcome-subtitle {
  font-size: 16px;
  line-height: 24px;
  font-weight: 400;
  color: rgba($on-surface-variant, 0.8);
  font-family: 'Hanken Grotesk', sans-serif;
}

/* Input Area */
.input-area {
  display: flex;
  flex-direction: column;
  gap: 32rpx;
  margin-top: 64rpx;
}

.input-wrapper {
  position: relative;
  display: flex;
  align-items: center;
}

.message-input {
  width: 100%;
  height: 128rpx;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 48rpx;
  padding: 0 48rpx;
  padding-right: 120rpx;
  font-size: 16px;
  font-weight: 400;
  font-family: 'Hanken Grotesk', sans-serif;
  color: $on-background;
  border: none;
  box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.03), 0 20rpx 80rpx rgba(0, 0, 0, 0.05);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);

  &::placeholder {
    color: $slate-400;
  }
}

.send-btn {
  position: absolute;
  right: 20rpx;
  width: 88rpx;
  height: 88rpx;
  border-radius: 24rpx;
  background: $primary;
  color: $on-primary;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 8rpx 24rpx rgba($primary, 0.25);

  &:active {
    transform: scale(0.95);
  }
}

.action-btns {
  display: flex;
  gap: 24rpx;
}

.voice-btn {
  flex: 1;
  height: 112rpx;
  border-radius: 48rpx;
  background: rgba(255, 255, 255, 0.6);
  color: $primary;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16rpx;
  border: 2rpx solid rgba($primary, 0.1);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.03), 0 20rpx 80rpx rgba(0, 0, 0, 0.05);

  &:active {
    transform: scale(0.95);
  }
}

.voice-btn-label {
  font-size: 14px;
  font-weight: 500;
  color: $primary;
}

.grid-btn {
  width: 112rpx;
  height: 112rpx;
  border-radius: 48rpx;
  background: rgba(255, 255, 255, 0.6);
  color: $on-surface-variant;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.03), 0 20rpx 80rpx rgba(0, 0, 0, 0.05);

  &:active {
    transform: scale(0.95);
  }
}

/* ===== Section Common ===== */
.section-title {
  font-size: 20px;
  line-height: 28px;
  font-weight: 600;
  color: $on-background;
  font-family: 'Hanken Grotesk', sans-serif;
}

/* ===== Today's Focus ===== */
.today-section {
  display: flex;
  flex-direction: column;
  gap: 40rpx;
}

.section-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.suggestion-badge {
  background: rgba($primary, 0.1);
  padding: 8rpx 24rpx;
  border-radius: 9999rpx;
}

.suggestion-badge-text {
  font-size: 12px;
  line-height: 16px;
  font-weight: 600;
  color: $primary;
  font-family: 'Geist', sans-serif;
}

.cards-scroll {
  width: 100%;
  white-space: nowrap;
}

.cards-row {
  display: flex;
  gap: 40rpx;
  padding-bottom: 16rpx;
  padding-left: 8rpx;
  padding-right: 8rpx;
}

/* Focus Cards */
.focus-card {
  flex-shrink: 0;
  min-width: 560rpx;
  padding: 40rpx;
  border-radius: 48rpx;
  display: flex;
  flex-direction: column;
  gap: 24rpx;

  &--primary {
    border-left: 8rpx solid $primary;
  }

  &--rose {
    background: rgba($slate-50, 0.8);
    border: 2rpx solid rgba($slate-200, 0.5);
    box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.05);
  }
}

.focus-card-head {
  display: flex;
  align-items: center;
  gap: 16rpx;
}

.focus-icon--primary {
  color: $primary;
}

.focus-icon--rose {
  color: $rose-500;
}

.focus-label--primary {
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: $primary;
  font-family: 'Geist', sans-serif;
}

.focus-label--rose {
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  color: $rose-500;
  font-family: 'Geist', sans-serif;
}

.focus-card-desc {
  font-size: 16px;
  line-height: 22px;
  font-weight: 400;
  color: $on-surface;
  font-family: 'Hanken Grotesk', sans-serif;
}

.focus-card-actions {
  display: flex;
  gap: 16rpx;
  padding-top: 24rpx;
}

.btn-primary {
  background: $primary;
  padding: 20rpx 48rpx;
  border-radius: 24rpx;
  box-shadow: 0 20rpx 30rpx rgba($primary, 0.2);

  &:active {
    transform: scale(0.95);
  }
}

.btn-primary-text {
  font-size: 14px;
  line-height: 20px;
  font-weight: 500;
  color: $on-primary;
  font-family: 'Geist', sans-serif;
}

.btn-secondary {
  background: $slate-100;
  padding: 20rpx 40rpx;
  border-radius: 24rpx;
}

.btn-secondary-text {
  font-size: 14px;
  line-height: 20px;
  font-weight: 500;
  color: $on-surface-variant;
  font-family: 'Geist', sans-serif;
}

.btn-outline {
  background: #ffffff;
  border: 2rpx solid $slate-200;
  padding: 20rpx 48rpx;
  border-radius: 24rpx;
  box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.05);

  &:active {
    transform: scale(0.95);
  }
}

.btn-outline-text {
  font-size: 14px;
  line-height: 20px;
  font-weight: 500;
  color: $on-surface;
  font-family: 'Geist', sans-serif;
}

/* ===== Timeline ===== */
.timeline-section {
  display: flex;
  flex-direction: column;
  gap: 64rpx;
}

.timeline {
  display: flex;
  flex-direction: column;
  gap: 64rpx;
  position: relative;
  padding-left: 0;

  &::before {
    content: '';
    position: absolute;
    left: 40rpx;
    top: 16rpx;
    bottom: 16rpx;
    width: 4rpx;
    background: $slate-100;
  }
}

.timeline-item {
  display: flex;
  gap: 40rpx;
  position: relative;
}

.timeline-dot {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  background: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;
  border: 4rpx solid $slate-100;
  box-shadow: 0 2rpx 4rpx rgba(0, 0, 0, 0.05);
  color: $slate-400;
  flex-shrink: 0;

  &--active {
    background: $primary;
    border-color: $primary-container;
    border-width: 8rpx;
    box-shadow: 0 8rpx 24rpx rgba($primary, 0.2);
    color: $on-primary;
  }
}

.timeline-info {
  padding-top: 4rpx;
  display: flex;
  flex-direction: column;
}

.timeline-time {
  font-size: 12px;
  line-height: 16px;
  font-weight: 500;
  color: $on-surface-variant;
  font-family: 'Geist', sans-serif;
}

.timeline-name {
  font-size: 16px;
  line-height: 24px;
  font-weight: 600;
  color: $on-surface;
  font-family: 'Hanken Grotesk', sans-serif;
}

.timeline-desc {
  font-size: 12px;
  line-height: 16px;
  color: rgba($on-surface-variant, 0.8);
  font-family: 'Geist', sans-serif;
}

/* Active Timeline Card */
.timeline-active-card {
  background: rgba($primary-container, 0.3) !important;
  border: 2rpx solid rgba($primary, 0.1);
  padding: 40rpx;
  border-radius: 48rpx;
  flex: 1;
  box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.06);
  display: flex;
  flex-direction: column;
  gap: 4rpx;
}

.timeline-active-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 4rpx;
}

.timeline-active-time {
  font-size: 12px;
  line-height: 16px;
  font-weight: 700;
  color: $primary;
  font-family: 'Geist', sans-serif;
}

.pulse-dot {
  width: 16rpx;
  height: 16rpx;
  border-radius: 50%;
  background: $primary;
  animation: breathe 2s ease-in-out infinite;
}

.timeline-active-name {
  font-size: 16px;
  line-height: 24px;
  font-weight: 700;
  color: $on-primary-container;
  font-family: 'Hanken Grotesk', sans-serif;
}

.timeline-active-desc {
  font-size: 12px;
  line-height: 16px;
  color: $on-surface-variant;
  font-family: 'Geist', sans-serif;
}

/* ===== Smart Services ===== */
.services-section {
  display: flex;
  flex-direction: column;
  gap: 40rpx;
}

.services-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 32rpx;
}

.service-card {
  background: linear-gradient(to bottom right, $slate-50, #ffffff);
  padding: 40rpx;
  border-radius: 64rpx;
  border: 2rpx solid rgba($slate-200, 0.6);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 320rpx;

  &:active {
    transform: scale(0.98);
  }
}

.service-icon {
  width: 96rpx;
  height: 96rpx;
  border-radius: 32rpx;
  display: flex;
  align-items: center;
  justify-content: center;

  &--orange {
    background: #fff7ed;
    color: $orange-500;
  }
  &--blue {
    background: #eff6ff;
    color: $blue-500;
  }
  &--green {
    background: #f0fdf4;
    color: $green-500;
  }
  &--purple {
    background: #faf5ff;
    color: $purple-500;
  }
}

.service-name {
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
  color: $on-surface;
  font-family: 'Geist', sans-serif;
}

/* Wide service items */
.service-wide {
  grid-column: span 2;
  background: rgba($slate-50, 0.5);
  padding: 40rpx;
  border-radius: 48rpx;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border: 2rpx solid rgba($slate-200, 0.4);

  &--danger {
    background: rgba(254, 242, 242, 0.5);
    border-color: rgba(#fecaca, 0.5);
  }
}

.service-wide-left {
  display: flex;
  align-items: center;
  gap: 32rpx;
}

.service-wide-icon {
  width: 80rpx;
  height: 80rpx;
  background: #ffffff;
  border-radius: 24rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2rpx solid $slate-100;
  color: $slate-400;

  &--danger {
    border-color: #fef2f2;
    color: $error;
  }
}

.service-wide-name {
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
  color: $on-surface;
  font-family: 'Geist', sans-serif;

  &--danger {
    color: $on-error-container;
  }
}

.service-wide-arrow {
  color: $slate-300;

  &--danger {
    color: rgba($error, 0.3);
  }
}

/* ===== Floating Action Chips ===== */
.floating-actions {
  position: fixed;
  bottom: 192rpx;
  left: 0;
  width: 100%;
  z-index: 40;
  padding: 0 48rpx;
}

.chips-scroll {
  width: 100%;
  white-space: nowrap;
}

.chips-row {
  display: flex;
  gap: 24rpx;
  padding-bottom: 16rpx;
}

.chip {
  flex: none;
  padding: 24rpx 40rpx;
  border-radius: 9999rpx;
  box-shadow: 0 8rpx 30rpx rgba(0, 0, 0, 0.08);
  display: flex;
  align-items: center;
  gap: 16rpx;
  background: rgba(255, 255, 255, 0.8) !important;
  border: 2rpx solid #ffffff;
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);

  &:active {
    transform: scale(0.95);
  }
}

.chip-icon {
  color: $primary;
}

.chip-text {
  font-size: 14px;
  line-height: 20px;
  font-weight: 500;
  color: $on-surface;
  font-family: 'Geist', sans-serif;
}

</style>
