<script>
export default {
  onLaunch() {
    // 字体在 index.html 中通过 link 标签加载
  }
}
</script>

<style>
/* ========== 全局重置与基础样式 ========== */
page {
  font-family: 'Hanken Grotesk', -apple-system, BlinkMacSystemFont, sans-serif;
  -webkit-font-smoothing: antialiased;
  background: #f7f9fb;
  color: #191c1e;
  -webkit-tap-highlight-color: transparent;
}

/* Material Symbols 字体 */
.material-symbols-outlined {
  font-family: 'Material Symbols Outlined';
  font-weight: normal;
  font-style: normal;
  font-size: 24px;
  line-height: 1;
  letter-spacing: normal;
  text-transform: none;
  display: inline-block;
  white-space: nowrap;
  word-wrap: normal;
  direction: ltr;
  font-variation-settings: 'FILL' 0, 'wght' 400, 'GRAD' 0, 'opsz' 24;
  -webkit-font-smoothing: antialiased;
}

/* 全局 Glassmorphism */
.glass-card {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
  border: 1px solid rgba(255, 255, 255, 0.4);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.03), 0 10px 40px rgba(0, 0, 0, 0.05);
}

/* Section Container (Butler 页面用的白底圆角卡片) */
.section-container {
  background: #ffffff;
  border-radius: 2rem;
  padding: 24px;
  border: 1px solid rgba(226, 232, 240, 0.6);
  box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.02);
}

/* 隐藏滚动条 */
.no-scrollbar::-webkit-scrollbar {
  display: none;
}
.no-scrollbar {
  -ms-overflow-style: none;
  scrollbar-width: none;
}

/* AI Orb 脉冲动画 */
@keyframes orb-pulse {
  0%, 100% { transform: scale(1); opacity: 1; box-shadow: 0 0 20px rgba(47, 155, 247, 0.5); }
  50% { transform: scale(1.1); opacity: 0.9; box-shadow: 0 0 35px rgba(47, 155, 247, 0.7); }
}
@keyframes ring-expand {
  0% { transform: scale(0.8); opacity: 0.6; }
  100% { transform: scale(1.8); opacity: 0; }
}

/* 脉冲指示器 */
@keyframes pulse-cyan {
  0%, 100% { box-shadow: 0 0 0 0 rgba(0, 97, 164, 0.4); }
  50% { box-shadow: 0 0 0 10px rgba(87, 223, 254, 0.2); }
}

/* 呼吸动画 (通用) */
@keyframes breathe {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

/* 入场动画 */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(15px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
