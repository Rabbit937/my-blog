<script setup>
import { ref } from 'vue'

const activeProject = ref(null)

const projects = [
  {
    id: 0,
    title: '电商小程序',
    category: 'AI',
    desc: 'Vibe Coding 开发的全栈电商小程序，uni-app + Bun + Hono + PostgreSQL',
    detail: '使用 Cursor + Claude Code vibe coding 开发的全栈电商小程序。前端使用 uni-app + Vue 3 + TypeScript，支持 H5 和微信小程序。后端使用 Bun + Hono + Drizzle ORM + PostgreSQL，使用 Docker 部署。功能包括：用户登录（短信验证码）、商品分类列表、购物车、订单管理、收货地址、用户收藏等。项目包含完整的高保真设计图和数据库设计文档。',
    tech: ['uni-app', 'Vue 3', 'TypeScript', 'Bun', 'Hono', 'Drizzle ORM', 'PostgreSQL', 'Docker'],
    github: ''
  },
  {
    id: 0,
    title: 'AI Workbench',
    category: 'AI',
    desc: 'Vibe Coding 开发的 AI 知识库助手，展示 RAG、MCP、Memory 等功能',
    detail: '使用 Cursor + Claude Code vibe coding 开发的 AI 全栈项目。功能：本地文档知识库管理，基于关键词检索的 RAG 问答，聊天记录来源引用，支持 OpenAI 兼容 API（可切换 GPT/Claude 等模型）。技术栈：React + TypeScript 前端，Bun + Elysia 后端，JSON 本地持久化。这个项目展示了 AI 应用开发能力，理解 RAG、MCP、Skills、Function Calling 等概念。',
    tech: ['React', 'TypeScript', 'Bun', 'Elysia', 'RAG', 'MCP'],
    github: 'https://github.com/Rabbit937/ai-workbench'
  },
  {
    id: 1,
    title: 'Solana DEX DApp',
    category: 'Web3',
    desc: '基于 Solana 链的去中心化交易所，实现代币 swap、流动性池功能',
    detail: '独立开发的 Solana DEX 前端，采用 React + TypeScript 构建。实现了代币兑换、流动性池添加/移除等核心 DeFi 功能。集成 @solana/wallet-adapter-react 实现多钱包连接（Phantom、Solflare 等）。调用 SPL Token 合约进行代币余额查询、转账、兑换操作。配合后端服务实现价格聚合和交易滑点计算。',
    tech: ['React', 'Solana', 'Web3.js', 'TypeScript', 'Tailwind'],
    github: 'https://github.com/Rabbit937'
  },
  {
    id: 2,
    title: 'Binance 公告监听推送机器人',
    category: 'Web3',
    desc: 'Rust 开发的币安公告实时监听，推送到 Telegram',
    detail: '使用 Rust 开发的币安公告实时监听程序。主要功能：定时抓取币安官网公告页面，解析 HTML 获取最新上币/活动信息，设计消息队列机制将公告推送到指定 Telegram 频道，实现定时轮询+增量更新减少无效请求，使用 tokio 异步 runtime 保证高并发性能。',
    tech: ['Rust', 'reqwest', 'teloxide', 'Telegram API', 'tokio'],
    github: 'https://github.com/Rabbit937'
  },
  {
    id: 3,
    title: '广告买量系统',
    category: '工作',
    company: '九月稻田',
    desc: 'Vue3 + TypeScript 构建的自动化广告投放管理后台',
    detail: '负责广告买量系统前端开发。技术栈：Vue3 + Vite + TypeScript + Element Plus。使用 Vuex 进行状态管理，Vue Router 进行路由控制，Axios 封装请求拦截。实现多平台广告投放功能，支持创建、推送、暂停、删除等操作，覆盖广告类型、平台、渠道、位置、素材等多种维度配置。参与项目国际化（vue-i18n），优化构建配置（vite-plugin-html、vite-plugin-compression）。独立完成需求评审、页面开发、联调测试和上线部署。',
    tech: ['Vue3', 'TypeScript', 'Vite', 'Element Plus', 'Vuex', 'vue-i18n'],
    github: ''
  },
  {
    id: 4,
    title: 'TikTok 弹幕捕捉桌面端',
    category: '工作',
    company: '602游戏',
    desc: 'Electron 开发的 TikTok 直播弹幕实时捕捉工具',
    detail: '使用 Electron 开发的桌面端工具，用于捕捉 TikTok 直播弹幕数据。主要工作：分析 TikTok 网页结构和通信协议，设计弹幕数据捕捉方案，解析 WebSocket 协议获取实时弹幕数据，将数据转发到后端服务器，最终封装为可交付的 exe 应用程序。',
    tech: ['Electron', 'WebSocket', '数据解析', 'Node.js'],
    github: ''
  },
  {
    id: 5,
    title: 'H5 游戏发行 SDK',
    category: '工作',
    company: '602游戏',
    desc: '为游戏研发方提供的一站式发行 SDK',
    detail: '负责游戏发行 SDK 的前端开发与维护。封装统一的 JavaScript 接口供游戏研发接入。设计并实现与 CP（游戏研发）的通信方式，对接微信支付和支付宝支付，完成移动端横竖屏适配，以及 iOS/Android 壳包通信。编写清晰的 SDK 文档供接入方使用。',
    tech: ['JavaScript', 'TypeScript', '支付对接', 'Hybrid', '微信支付', '支付宝'],
    github: ''
  },
  {
    id: 6,
    title: '游戏充值公众号',
    category: '工作',
    company: '602游戏',
    desc: '微信开发者工具开发的游戏充值 H5 页面',
    detail: '使用微信开发者工具开发的公众号充值页面。负责前端页面开发和调试，对接公众号支付接口，处理各种浏览器兼容性问题。根据运营需求开发充值活动页面。',
    tech: ['JavaScript', '微信公众号', '支付对接', '微信开发者工具'],
    github: ''
  },
  {
    id: 7,
    title: '立白供应链管理系统',
    category: '工作',
    company: '嘉仕软件',
    desc: '基于 Vue 的网页版电子表格系统',
    detail: '参与立白供应链电子表格系统开发。负责物流信息的网页版电子表格展示，又称网页版 Excel。根据业务需求开发动态表格页面，实现公式计算和数据处理功能。针对表格类复杂场景进行性能优化，提升页面加载和交互流畅度。',
    tech: ['Vue', '动态表格', '数据处理', '性能优化'],
    github: ''
  },
  {
    id: 8,
    title: '顶点思维教育平台',
    category: '工作',
    company: '顶点思维教育',
    desc: '中小学在线教育平台，学生端/教师端/H5 移动端',
    detail: '参与中小学教育平台开发。学生端：基于 Vue + Vant 开发 H5 WebApp 移动端，使用 HBuilderX 打包为 App，调用 Android 原生能力（拍照、扫码）。教师端：实现与学生端的 Socket 通信，支持实时互动。后台：使用 ThinkPHP5 开发后台管理模块，负责接口联调和数据对接。',
    tech: ['Vue', 'Vant', 'Socket', 'PHP', 'ThinkPHP5', 'HBuilderX', 'Android'],
    github: ''
  }
]

const skills = {
  frontend: ['Vue2/Vue3', 'React', 'TypeScript', 'Vite', 'Element Plus', 'Vant', 'Electron'],
  backend: ['Node.js', 'Bun', 'Elysia', 'Go', 'Gin', 'Python', 'ThinkPHP5'],
  web3: ['Solidity', 'Rust', 'Solana', 'Web3.js', '智能合约'],
  tools: ['Cursor', 'Claude Code', 'Codex', 'Git', 'Jenkins', 'Docker']
}

const experience = [
  { time: '2024.08 - 至今', title: '个人项目 / 技术研究', company: '', desc: 'Web3 开发、全栈练习、AI 协同开发' },
  { time: '2024.03 - 2024.08', title: '前端开发工程师', company: '九月稻田', desc: '广告买量系统' },
  { time: '2021.10 - 2024.01', title: '前端开发工程师', company: '602游戏', desc: 'H5 SDK、充值系统、桌面端工具' },
  { time: '2021.03 - 2021.10', title: '前端开发工程师', company: '嘉仕软件', desc: '供应链系统' },
  { time: '2019.11 - 2021.03', title: '前端开发工程师', company: '顶点思维教育', desc: '教育平台' }
]

const showDetail = (project) => {
  activeProject.value = project
}

const closeDetail = () => {
  activeProject.value = null
}
</script>

<template>
  <div class="blog">
    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-bg"></div>
      <div class="hero-content">
        <div class="avatar">
          <span>🐰</span>
        </div>
        <h1>hackrabbit</h1>
        <p class="subtitle">前端开发工程师 | 4-5年经验 | 广州</p>
        <p class="intro">
          熟悉 Vue/React/TypeScript，有全栈开发能力。<br>
          擅长使用 Cursor + Claude Code 进行 Vibe Coding，最近做了 AI Workbench 和电商小程序两个全栈项目。
        </p>
        <div class="contact">
          <a href="https://github.com/Rabbit937" target="_blank" class="contact-item">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
            GitHub
          </a>
          <span class="contact-item">📍 广州</span>
          <span class="contact-item">📧 yly1773737856@gmail.com</span>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section class="section skills-section">
      <h2 class="section-title">
        <span class="icon">⚡</span>
        技术栈
      </h2>
      <div class="skills-grid">
        <div class="skill-card" v-for="(list, key) in skills" :key="key">
          <h3>{{ {frontend: '前端', backend: '后端', web3: 'Web3', tools: '工具'}[key] }}</h3>
          <div class="skill-tags">
            <span v-for="s in list" :key="s">{{ s }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section class="section projects-section">
      <h2 class="section-title">
        <span class="icon">🚀</span>
        项目经历
      </h2>
      <div class="projects-grid">
        <div
          v-for="p in projects"
          :key="p.id"
          class="project-card"
          :class="p.category"
          @click="showDetail(p)"
        >
          <div class="project-badge">{{ p.category }}</div>
          <h3>{{ p.title }}</h3>
          <p class="project-company" v-if="p.company">{{ p.company }}</p>
          <p class="project-desc">{{ p.desc }}</p>
          <div class="project-tags">
            <span v-for="t in p.tech.slice(0, 3)" :key="t">{{ t }}</span>
          </div>
          <div class="project-hover">
            <span>查看详情 →</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section class="section experience-section">
      <h2 class="section-title">
        <span class="icon">💼</span>
        工作经历
      </h2>
      <div class="experience-timeline">
        <div class="exp-item" v-for="(exp, i) in experience" :key="i">
          <div class="exp-time">{{ exp.time }}</div>
          <div class="exp-dot"></div>
          <div class="exp-content">
            <h3>{{ exp.title }}</h3>
            <p class="exp-company" v-if="exp.company">{{ exp.company }}</p>
            <p class="exp-desc">{{ exp.desc }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <p>© 2024 hackrabbit. Built with Vue 3 + Vite.</p>
    </footer>

    <!-- Modal -->
    <Transition name="fade">
      <div class="modal-overlay" v-if="activeProject" @click="closeDetail">
        <div class="modal-content" @click.stop>
          <button class="modal-close" @click="closeDetail">×</button>
          <div class="modal-badge">{{ activeProject.category }}</div>
          <h2>{{ activeProject.title }}</h2>
          <p class="modal-company" v-if="activeProject.company">{{ activeProject.company }}</p>
          <p class="modal-detail">{{ activeProject.detail }}</p>
          <div class="modal-tags">
            <span v-for="t in activeProject.tech" :key="t">{{ t }}</span>
          </div>
          <a v-if="activeProject.github" :href="activeProject.github" target="_blank" class="modal-github">
            <svg viewBox="0 0 24 24" width="18" height="18" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
            查看源码
          </a>
        </div>
      </div>
    </Transition>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  background: #0a0a0f;
  color: #e4e4e7;
  line-height: 1.6;
}

.blog {
  min-height: 100vh;
}

/* Hero */
.hero {
  position: relative;
  padding: 100px 20px 60px;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse at 20% 20%, rgba(99, 102, 241, 0.15) 0%, transparent 50%),
    radial-gradient(ellipse at 80% 80%, rgba(168, 85, 247, 0.1) 0%, transparent 50%),
    linear-gradient(180deg, #0a0a0f 0%, #13131a 100%);
}

.hero-content {
  position: relative;
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

.avatar {
  width: 100px;
  height: 100px;
  background: linear-gradient(135deg, #6366f1 0%, #a855f7 100%);
  border-radius: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 24px;
  font-size: 48px;
  box-shadow: 0 20px 40px rgba(99, 102, 241, 0.3);
}

.hero h1 {
  font-size: 42px;
  font-weight: 700;
  margin-bottom: 8px;
  background: linear-gradient(135deg, #fff 0%, #a1a1aa 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.subtitle {
  color: #71717a;
  font-size: 16px;
  margin-bottom: 16px;
}

.intro {
  color: #a1a1aa;
  font-size: 14px;
  margin-bottom: 24px;
  line-height: 1.8;
}

.contact {
  display: flex;
  justify-content: center;
  gap: 24px;
  flex-wrap: wrap;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 6px;
  color: #a1a1aa;
  font-size: 14px;
  text-decoration: none;
  transition: color 0.2s;
}

.contact-item:hover {
  color: #6366f1;
}

/* Section */
.section {
  max-width: 1000px;
  margin: 0 auto;
  padding: 60px 20px;
}

.section-title {
  font-size: 24px;
  font-weight: 600;
  margin-bottom: 32px;
  display: flex;
  align-items: center;
  gap: 12px;
}

.section-title .icon {
  font-size: 28px;
}

/* Skills */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
}

.skill-card {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 12px;
  padding: 20px;
}

.skill-card h3 {
  font-size: 14px;
  color: #6366f1;
  margin-bottom: 12px;
  font-weight: 500;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.skill-tags span {
  background: rgba(99, 102, 241, 0.1);
  color: #a5b4fc;
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 12px;
}

/* Projects */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}

.project-card {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 16px;
  padding: 24px;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.project-card:hover {
  transform: translateY(-4px);
  border-color: rgba(99, 102, 241, 0.3);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.project-card.Web3 {
  border-left: 3px solid #a855f7;
}

.project-card.AI {
  border-left: 3px solid #10b981;
}

.project-card.工作 {
  border-left: 3px solid #6366f1;
}

.project-badge {
  position: absolute;
  top: 16px;
  right: 16px;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding: 4px 8px;
  border-radius: 4px;
  background: rgba(99, 102, 241, 0.1);
  color: #a5b4fc;
}

.project-card.Web3 .project-badge {
  background: rgba(168, 85, 247, 0.1);
  color: #c4b5fd;
}

.project-card.AI .project-badge {
  background: rgba(16, 185, 129, 0.1);
  color: #6ee7b7;
}

.project-card h3 {
  font-size: 18px;
  margin-bottom: 4px;
  padding-right: 60px;
}

.project-company {
  font-size: 13px;
  color: #71717a;
  margin-bottom: 12px;
}

.project-desc {
  color: #a1a1aa;
  font-size: 14px;
  margin-bottom: 16px;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.project-tags span {
  background: rgba(255, 255, 255, 0.05);
  color: #71717a;
  padding: 3px 8px;
  border-radius: 4px;
  font-size: 11px;
}

.project-hover {
  position: absolute;
  inset: 0;
  background: rgba(99, 102, 241, 0.9);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s;
}

.project-card:hover .project-hover {
  opacity: 1;
}

.project-hover span {
  color: white;
  font-weight: 500;
}

/* Experience */
.experience-timeline {
  position: relative;
  padding-left: 30px;
}

.experience-timeline::before {
  content: '';
  position: absolute;
  left: 6px;
  top: 8px;
  bottom: 8px;
  width: 2px;
  background: linear-gradient(180deg, #6366f1 0%, #a855f7 100%);
}

.exp-item {
  position: relative;
  padding-bottom: 32px;
}

.exp-item:last-child {
  padding-bottom: 0;
}

.exp-dot {
  position: absolute;
  left: -30px;
  top: 8px;
  width: 14px;
  height: 14px;
  background: #6366f1;
  border-radius: 50%;
  box-shadow: 0 0 0 4px rgba(99, 102, 241, 0.2);
}

.exp-time {
  font-size: 13px;
  color: #71717a;
  margin-bottom: 4px;
}

.exp-content h3 {
  font-size: 16px;
  margin-bottom: 2px;
}

.exp-company {
  font-size: 14px;
  color: #a855f7;
  margin-bottom: 4px;
}

.exp-desc {
  font-size: 14px;
  color: #a1a1aa;
}

/* Footer */
.footer {
  text-align: center;
  padding: 40px 20px;
  color: #52525b;
  font-size: 13px;
}

/* Modal */
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  z-index: 100;
  backdrop-filter: blur(4px);
}

.modal-content {
  background: #18181b;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 32px;
  max-width: 600px;
  width: 100%;
  max-height: 80vh;
  overflow-y: auto;
  position: relative;
}

.modal-close {
  position: absolute;
  top: 16px;
  right: 16px;
  width: 32px;
  height: 32px;
  border: none;
  background: rgba(255, 255, 255, 0.1);
  color: #a1a1aa;
  border-radius: 8px;
  font-size: 20px;
  cursor: pointer;
  transition: all 0.2s;
}

.modal-close:hover {
  background: rgba(255, 255, 255, 0.2);
  color: #fff;
}

.modal-badge {
  display: inline-block;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  padding: 4px 10px;
  border-radius: 4px;
  background: rgba(99, 102, 241, 0.1);
  color: #a5b4fc;
  margin-bottom: 12px;
}

.modal-content h2 {
  font-size: 24px;
  margin-bottom: 4px;
}

.modal-company {
  color: #a855f7;
  margin-bottom: 20px;
}

.modal-detail {
  color: #d4d4d8;
  line-height: 1.8;
  margin-bottom: 20px;
}

.modal-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 20px;
}

.modal-tags span {
  background: rgba(255, 255, 255, 0.05);
  color: #a1a1aa;
  padding: 6px 12px;
  border-radius: 6px;
  font-size: 13px;
}

.modal-github {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  color: #fff;
  text-decoration: none;
  background: #2563eb;
  padding: 10px 20px;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 500;
  transition: background 0.2s;
}

.modal-github:hover {
  background: #1d4ed8;
}

/* Transition */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 640px) {
  .hero h1 {
    font-size: 32px;
  }

  .contact {
    flex-direction: column;
    gap: 12px;
  }

  .skills-grid {
    grid-template-columns: 1fr;
  }

  .projects-grid {
    grid-template-columns: 1fr;
  }
}
</style>
