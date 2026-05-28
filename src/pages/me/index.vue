<template>
  <view class="page">
    <!-- TopAppBar -->
    <view class="header" :style="{ paddingTop: statusBarHeight + 'px' }">
      <view class="header-inner">
        <view class="header-left">
          <view class="avatar-wrap">
            <view class="avatar">
              <image
                class="avatar-img"
                src="https://lh3.googleusercontent.com/aida-public/AB6AXuBMOzovkXHUEToc2vrMwJjF-T20PKqdzQhwm9IYlijmEIYXHz8p4stnBM8H3sbw1cNXYiUipI4Dybu_ikPOEnz7u0r7tEthB7A0PCrmo9VRjYEShsS-gPp2VM3H6sawW86yOLdylUcYty1_dIRkeqqzwWKS2uDNypJCsxgacSFp6JzE1fJQ2CdfTp2iHKx-rjVs6-5eYMnig49BlIXNu20Sp1SKAJjf-ubggt97qXuxghdDvmbsb88BPSDZHn7MoDfD_FkH6Y5attc"
                mode="aspectFill"
              />
            </view>
            <view class="online-dot" />
          </view>
          <text class="header-title">OpenClaw</text>
        </view>
        <view class="notify-btn">
          <text class="icon-font notify-icon">notifications</text>
        </view>
      </view>
    </view>

    <!-- Main Content -->
    <view class="main">
      <!-- Profile Header -->
      <view class="profile-section">
        <text class="welcome-text">欢迎回来，Alex</text>
        <view class="steward-badge">
          <text class="badge-text">管家状态：活跃</text>
        </view>
      </view>

      <!-- AI Memories Card -->
      <view class="card">
        <view class="card-header">
          <view class="card-header-left">
            <view class="icon-box icon-box-primary">
              <text class="icon-font card-icon">psychology</text>
            </view>
            <text class="card-title">AI 记忆库</text>
          </view>
          <view class="manage-btn">
            <text class="manage-btn-text">管理</text>
          </view>
        </view>
        <view class="memory-grid">
          <view class="memory-item">
            <text class="memory-label">饮食偏好</text>
            <text class="memory-value">低碳水，鱼素</text>
          </view>
          <view class="memory-item">
            <text class="memory-label">过敏源</text>
            <text class="memory-value memory-value-error">花生，贝类</text>
          </view>
          <view class="memory-item memory-item-full">
            <text class="memory-label">常去地点</text>
            <text class="memory-value">Equinox, Blue Bottle, 中央公园</text>
          </view>
          <view class="memory-item memory-item-full">
            <text class="memory-label">家庭信息</text>
            <text class="memory-value">Sophie (妻), Leo (子, 4岁)</text>
          </view>
        </view>
      </view>

      <!-- Recent Activity Card -->
      <view class="card">
        <view class="card-header">
          <view class="card-header-left">
            <view class="icon-box icon-box-secondary">
              <text class="icon-font card-icon">history</text>
            </view>
            <text class="card-title">最近动态</text>
          </view>
        </view>
        <view class="activity-list">
          <view class="activity-item" @tap="onActivityTap(0)">
            <view class="activity-left">
              <view class="activity-icon-wrap activity-icon-primary">
                <text class="icon-font activity-icon">lunch_dining</text>
              </view>
              <view class="activity-info">
                <text class="activity-title">外卖：中泽寿司</text>
                <text class="activity-sub">2小时前 • $84.20</text>
              </view>
            </view>
          </view>
          <view class="activity-item" @tap="onActivityTap(1)">
            <view class="activity-left">
              <view class="activity-icon-wrap activity-icon-secondary">
                <text class="icon-font activity-icon">local_taxi</text>
              </view>
              <view class="activity-info">
                <text class="activity-title">打车：家 -> 浦东机场</text>
                <text class="activity-sub">昨天 • AI 安排</text>
              </view>
            </view>
          </view>
          <view class="activity-item" @tap="onActivityTap(2)">
            <view class="activity-left">
              <view class="activity-icon-wrap activity-icon-tertiary">
                <text class="icon-font activity-icon">cleaning_services</text>
              </view>
              <view class="activity-info">
                <text class="activity-title">家政：全屋深度保洁</text>
                <text class="activity-sub">周五 10:00 AM</text>
              </view>
            </view>
          </view>
        </view>
      </view>

      <!-- Service Management Card -->
      <view class="card">
        <view class="card-header">
          <view class="card-header-left">
            <view class="icon-box icon-box-container">
              <text class="icon-font card-icon">settings_suggest</text>
            </view>
            <text class="card-title">服务管理</text>
          </view>
        </view>
        <view class="switch-list">
          <view class="switch-item">
            <text class="switch-label">24/7 主动管家</text>
            <switch :checked="serviceSteward" color="#2f9bf7" @change="onSwitchSteward" />
          </view>
          <view class="switch-item">
            <text class="switch-label">主动提醒</text>
            <switch :checked="serviceReminder" color="#2f9bf7" @change="onSwitchReminder" />
          </view>
        </view>
      </view>

      <!-- Privacy & Security Card -->
      <view class="card">
        <view class="card-header">
          <view class="card-header-left">
            <view class="icon-box icon-box-outline">
              <text class="icon-font card-icon">shield</text>
            </view>
            <text class="card-title">隐私安全</text>
          </view>
        </view>
        <view class="privacy-list">
          <view class="privacy-item" @tap="onPrivacyTap('storage')">
            <text class="privacy-label">本地知识存储</text>
            <view class="privacy-right">
              <view class="tag-on">
                <text class="tag-on-text">已开启</text>
              </view>
            </view>
          </view>
          <view class="privacy-item privacy-item-border" @tap="onPrivacyTap('export')">
            <text class="privacy-label">数据导出与迁移</text>
            <text class="icon-font chevron-icon">chevron_right</text>
          </view>
        </view>
      </view>

      <!-- General Settings Card -->
      <view class="card">
        <view class="card-header">
          <view class="card-header-left">
            <view class="icon-box icon-box-outline">
              <text class="icon-font card-icon">palette</text>
            </view>
            <text class="card-title">通用设置</text>
          </view>
        </view>
        <view class="theme-row">
          <text class="switch-label">外观模式</text>
          <view class="theme-btn-group">
            <view
              class="theme-btn"
              :class="{ 'theme-btn-active': themeMode === 'light' }"
              @tap="setTheme('light')"
            >
              <text class="icon-font theme-btn-icon">light_mode</text>
            </view>
            <view
              class="theme-btn"
              :class="{ 'theme-btn-active': themeMode === 'dark' }"
              @tap="setTheme('dark')"
            >
              <text class="icon-font theme-btn-icon">dark_mode</text>
            </view>
            <view
              class="theme-btn"
              :class="{ 'theme-btn-active': themeMode === 'auto' }"
              @tap="setTheme('auto')"
            >
              <text class="icon-font theme-btn-icon">brightness_auto</text>
            </view>
          </view>
        </view>
      </view>

      <!-- Sign Out -->
      <view class="sign-out-wrap">
        <view class="sign-out-btn" @tap="onSignOut">
          <text class="icon-font sign-out-icon">logout</text>
          <text class="sign-out-text">安全退出登录</text>
        </view>
      </view>
    </view>

    <!-- Bottom Nav Bar (visual only) -->
    <view class="bottom-nav">
      <view class="nav-item">
        <text class="icon-font nav-icon nav-icon-inactive">smart_toy</text>
        <text class="nav-label nav-label-inactive">管家</text>
      </view>
      <view class="nav-item">
        <text class="icon-font nav-icon nav-icon-inactive">shopping_bag</text>
        <text class="nav-label nav-label-inactive">商城</text>
      </view>
      <view class="nav-item">
        <text class="icon-font nav-icon nav-icon-inactive">construction</text>
        <text class="nav-label nav-label-inactive">工具</text>
      </view>
      <view class="nav-item">
        <text class="icon-font nav-icon nav-icon-active">person</text>
        <text class="nav-label nav-label-active">我的</text>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const statusBarHeight = ref(0)
const serviceSteward = ref(true)
const serviceReminder = ref(true)
const themeMode = ref('light')

onMounted(() => {
  const systemInfo = uni.getSystemInfoSync()
  statusBarHeight.value = systemInfo.statusBarHeight || 20
})

function onSwitchSteward(e) {
  serviceSteward.value = e.detail.value
}

function onSwitchReminder(e) {
  serviceReminder.value = e.detail.value
}

function setTheme(mode) {
  themeMode.value = mode
}

function onActivityTap(index) {
  // noop – visual only
}

function onPrivacyTap(type) {
  // noop – visual only
}

function onSignOut() {
  // noop – visual only
}
</script>

<style lang="scss" scoped>
/* ---------- Design Tokens ---------- */
$primary: #0061a4;
$primary-container: #2f9bf7;
$primary-fixed: #d1e4ff;
$secondary: #00687a;
$secondary-container: #57dffe;
$tertiary: #494bd6;
$tertiary-container: #878bff;
$error: #ba1a1a;
$surface: #f7f9fb;
$surface-container: #eceef0;
$surface-container-low: #f2f4f6;
$surface-container-lowest: #ffffff;
$surface-container-high: #e6e8ea;
$on-surface: #191c1e;
$on-surface-variant: #404752;
$outline: #707883;
$outline-variant: #bfc7d4;

/* ---------- Page ---------- */
.page {
  min-height: 100vh;
  background-color: $surface-container;
  color: $on-surface;
  font-family: 'Hanken Grotesk', sans-serif;
  font-size: 16px;
  line-height: 24px;
}

/* ---------- Glass Header ---------- */
.header {
  position: sticky;
  top: 0;
  z-index: 50;
  background: rgba(247, 249, 251, 0.7);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  border-bottom: 2rpx solid rgba($outline-variant, 0.1);
}

.header-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 128rpx;
  padding: 0 40rpx;
}

.header-left {
  display: flex;
  align-items: center;
  gap: 24rpx;
}

.avatar-wrap {
  position: relative;
}

.avatar {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  background-color: $primary-fixed;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  box-shadow: inset 0 2rpx 4rpx rgba(0, 0, 0, 0.1);
  animation: pulseCyan 3s infinite ease-in-out;
}

@keyframes pulseCyan {
  0%, 100% { box-shadow: 0 0 0 0 rgba(0, 97, 164, 0.4); }
  50% { box-shadow: 0 0 0 20rpx rgba(87, 223, 254, 0.2); }
}

.avatar-img {
  width: 100%;
  height: 100%;
}

.online-dot {
  position: absolute;
  bottom: -2rpx;
  right: -2rpx;
  width: 24rpx;
  height: 24rpx;
  border-radius: 50%;
  background-color: $secondary;
  border: 4rpx solid $surface;
}

.header-title {
  font-family: 'Hanken Grotesk', sans-serif;
  font-size: 20px;
  font-weight: 700;
  color: $primary;
}

.notify-btn {
  width: 72rpx;
  height: 72rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 50%;
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.05);
}

.notify-icon {
  font-size: 40rpx;
  color: $primary;
}

/* ---------- Icon Font (Material Symbols Outlined) ---------- */
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
  font-variation-settings: 'FILL' 0, 'wght' 400, 'GRAD' 0, 'opsz' 24;
}

/* ---------- Main ---------- */
.main {
  padding: 48rpx 40rpx 200rpx;
}

/* ---------- Profile Section ---------- */
.profile-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 32rpx 0;
  gap: 32rpx;
}

.welcome-text {
  font-family: 'Hanken Grotesk', sans-serif;
  font-size: 24px;
  font-weight: 700;
  line-height: 64rpx;
  color: $on-surface;
}

.steward-badge {
  display: flex;
  align-items: center;
  gap: 16rpx;
  padding: 12rpx 32rpx;
  background: rgba($primary, 0.05);
  border-radius: 9999rpx;
  border: 2rpx solid rgba($primary, 0.1);
}

.badge-text {
  font-size: 14px;
  font-weight: 500;
  color: $primary-container;
}

/* ---------- Card ---------- */
.card {
  background-color: $surface-container-lowest;
  border-radius: 50rpx;
  padding: 48rpx;
  margin-top: 48rpx;
  box-shadow: 0 2rpx 6rpx rgba(0, 0, 0, 0.05), 0 20rpx 30rpx -10rpx rgba(0, 0, 0, 0.03), 0 8rpx 12rpx -4rpx rgba(0, 0, 0, 0.02);
  border: 2rpx solid #ffffff;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 48rpx;
}

.card-header-left {
  display: flex;
  align-items: center;
  gap: 16rpx;
}

.icon-box {
  padding: 12rpx;
  border-radius: 16rpx;
}

.icon-box-primary {
  background: rgba($primary, 0.1);
}

.icon-box-secondary {
  background: rgba($secondary, 0.1);
}

.icon-box-container {
  background: rgba($primary-container, 0.2);
}

.icon-box-outline {
  background: rgba($outline, 0.1);
}

.card-icon {
  font-size: 40rpx;
  color: $primary;
}

.icon-box-secondary .card-icon {
  color: $secondary;
}

.icon-box-container .card-icon {
  color: $primary-container;
}

.icon-box-outline .card-icon {
  color: $outline;
}

.card-title {
  font-family: 'Hanken Grotesk', sans-serif;
  font-size: 18px;
  font-weight: 700;
  color: $on-surface;
}

.manage-btn {
  padding: 8rpx 24rpx;
  background: rgba($primary, 0.05);
  border-radius: 9999rpx;
}

.manage-btn-text {
  font-size: 14px;
  font-weight: 500;
  color: $primary-container;
}

/* ---------- Memory Grid ---------- */
.memory-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 48rpx 48rpx;
}

.memory-item {
  width: calc(50% - 24rpx);
  display: flex;
  flex-direction: column;
  gap: 8rpx;
}

.memory-item-full {
  width: 100%;
}

.memory-label {
  font-size: 12px;
  font-weight: 600;
  color: $outline;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.memory-value {
  font-size: 16px;
  font-weight: 500;
  color: $on-surface;
}

.memory-value-error {
  color: $error;
}

/* ---------- Activity List ---------- */
.activity-list {
  display: flex;
  flex-direction: column;
  gap: 48rpx;
}

.activity-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin: -8rpx -16rpx;
  padding: 8rpx 16rpx;
  border-radius: 24rpx;
}

.activity-left {
  display: flex;
  align-items: center;
  gap: 32rpx;
}

.activity-icon-wrap {
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.activity-icon-primary {
  background: rgba($primary, 0.05);
}

.activity-icon-secondary {
  background: rgba($secondary, 0.05);
}

.activity-icon-tertiary {
  background: rgba($tertiary, 0.05);
}

.activity-icon {
  font-size: 40rpx;
}

.activity-icon-primary .activity-icon {
  color: rgba($primary, 0.7);
}

.activity-icon-secondary .activity-icon {
  color: rgba($secondary, 0.7);
}

.activity-icon-tertiary .activity-icon {
  color: rgba($tertiary, 0.7);
}

.activity-info {
  display: flex;
  flex-direction: column;
}

.activity-title {
  font-size: 16px;
  font-weight: 600;
  color: $on-surface;
}

.activity-sub {
  font-size: 12px;
  color: $on-surface-variant;
}

/* ---------- Switch List ---------- */
.switch-list {
  display: flex;
  flex-direction: column;
  gap: 32rpx;
}

.switch-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16rpx 0;
}

.switch-label {
  font-size: 16px;
  font-weight: 500;
  color: $on-surface;
}

/* ---------- Privacy List ---------- */
.privacy-list {
  display: flex;
  flex-direction: column;
}

.privacy-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 24rpx 0;
}

.privacy-item-border {
  border-top: 2rpx solid rgba($outline-variant, 0.1);
}

.privacy-label {
  font-size: 16px;
  font-weight: 500;
  color: $on-surface;
}

.privacy-right {
  display: flex;
  align-items: center;
  gap: 16rpx;
}

.tag-on {
  padding: 4rpx 16rpx;
  background: rgba($primary, 0.05);
  border-radius: 8rpx;
}

.tag-on-text {
  font-size: 12px;
  font-weight: 500;
  color: $primary-container;
}

.chevron-icon {
  font-size: 28rpx;
  color: $outline;
}

/* ---------- Theme Row ---------- */
.theme-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16rpx 0;
}

.theme-btn-group {
  display: flex;
  padding: 8rpx;
  background: $surface-container-low;
  border-radius: 24rpx;
  gap: 8rpx;
  box-shadow: inset 0 2rpx 4rpx rgba(0, 0, 0, 0.05);
  border: 2rpx solid rgba($outline-variant, 0.1);
}

.theme-btn {
  width: 72rpx;
  height: 72rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 16rpx;
  transition: all 0.2s;
}

.theme-btn-icon {
  font-size: 40rpx;
  color: $on-surface-variant;
}

.theme-btn-active {
  background: #ffffff;
  box-shadow: 0 2rpx 8rpx rgba(0, 0, 0, 0.08);
}

.theme-btn-active .theme-btn-icon {
  color: $primary;
}

/* ---------- Sign Out ---------- */
.sign-out-wrap {
  margin-top: 64rpx;
}

.sign-out-btn {
  width: 100%;
  padding: 32rpx 0;
  background: $surface-container-lowest;
  border-radius: 50rpx;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16rpx;
  box-shadow: 0 8rpx 40rpx rgba(0, 0, 0, 0.05);
  border: 2rpx solid rgba($error, 0.1);
}

.sign-out-btn:active {
  transform: scale(0.98);
}

.sign-out-icon {
  font-size: 40rpx;
  color: $error;
}

.sign-out-text {
  font-size: 14px;
  font-weight: 700;
  color: $error;
}

/* ---------- Bottom Nav ---------- */
.bottom-nav {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  z-index: 50;
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 16rpx 32rpx 48rpx;
  background: rgba(247, 249, 251, 0.7);
  backdrop-filter: blur(24rpx);
  -webkit-backdrop-filter: blur(24rpx);
  border-top: 2rpx solid rgba($outline-variant, 0.2);
  box-shadow: 0 -8rpx 24rpx rgba(0, 0, 0, 0.03);
}

.nav-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 8rpx 32rpx;
}

.nav-icon {
  font-size: 48rpx;
}

.nav-icon-inactive {
  color: rgba($on-surface-variant, 0.4);
}

.nav-icon-active {
  color: $primary-container;
}

.nav-label {
  font-size: 12px;
  margin-top: 4rpx;
}

.nav-label-inactive {
  color: rgba($on-surface-variant, 0.4);
}

.nav-label-active {
  color: $primary-container;
  font-weight: 700;
}
</style>
