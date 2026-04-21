<template>
  <div class="landing-page">
    <!-- Navbar -->
    <nav class="navbar">
      <div class="nav-logo">
        <span class="logo-icon">⎇</span>
        <span class="logo-text">seen</span>
      </div>
      <div class="nav-links">
        <a href="#features">{{ t.navFeatures }}</a>
        <a href="#demo">{{ t.navKey }}</a>
        <a href="#install">{{ t.navInstall }}</a>
        <a style="cursor: pointer;" class="lang-toggle" @click="toggleLang" :title="lang === 'zh' ? 'Switch to English' : '切换到中文'">
          {{ lang === 'zh' ? '简体中文' : 'EN' }}
        </a>
        <a href="https://github.com" target="_blank" class="github-link">
          <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor">
            <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
          </svg>
          GitHub
        </a>
      </div>
    </nav>

    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <div class="badge">{{ t.heroBadge }}</div>
        <h1 class="hero-title">
          {{ t.heroTitle1 }} <span class="highlight">{{ t.highlight || 'TUI' }}</span><br />
          {{ t.heroTitle2 }}
        </h1>
        <p class="hero-desc">
          {{ t.heroDesc1 }}<br />
          {{ t.heroDesc2 }}
        </p>
        <div class="hero-actions">
          <div class="hero-cmd">
            <span class="hero-cmd-prompt">$</span>
            <span class="hero-cmd-text">npx @seen-tui/cli</span>
            <button class="hero-cmd-copy" @click="copyCmd" :class="{ copied: cmdCopied }">
              {{ cmdCopied ? t.copiedBtn : t.copyBtn }}
            </button>
          </div>
          <a href="https://github.com/zzlorz/seen" target="_blank" class="hero-github-btn">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/>
            </svg>
            zzlorz/seen
          </a>
        </div>
        <div class="hero-meta">
          <span class="meta-item">
            <span class="meta-dot green"></span> {{ t.metaRust }}
          </span>
          <span class="meta-item">
            <span class="meta-dot orange"></span> {{ t.metaPlatform }}
          </span>
          <span class="meta-item">
            <span class="meta-dot blue"></span> {{ t.metaLicense }}
          </span>
        </div>
      </div>

      <!-- Terminal Preview -->
      <div class="terminal-wrapper">
        <div class="terminal">
          <div class="terminal-titlebar">
            <span class="dot red"></span>
            <span class="dot yellow"></span>
            <span class="dot green-dot"></span>
            <span class="terminal-title">{{ t.terminalTitle }}</span>
          </div>
          <div class="terminal-tabs">
            <span class="tab active">1 {{ t.tabGit }}</span>
            <span class="tab">2 {{ t.tabGraph }}</span>
          </div>
          <div class="terminal-body">
            <div class="panel-left">
              <div class="panel-header">{{ t.panelFiles }}</div>
              <div class="panel-subheader untracked">{{ t.panelUntracked }}</div>
              <div class="file-item active-file">?? .gitignore</div>
              <div class="file-item">?? Cargo.lock</div>
              <div class="file-item">?? Cargo.toml</div>
              <div class="file-item">?? src/</div>
            </div>
            <div class="panel-divider"></div>
            <div class="panel-right">
              <div class="diff-line">
                <span class="diff-filename">.gitignore</span>
                <span class="diff-tag">· untracked · ??</span>
              </div>
              <div class="diff-info">{{ t.diffUntracked }}</div>
              <div class="diff-info muted">{{ t.diffMuted }}</div>
            </div>
          </div>
          <div class="terminal-statusbar">
            <span class="status-hint">{{ t.statusHint1 }}</span>
            <span class="status-hint">{{ t.statusHint2 }}</span>
            <span class="status-hint">{{ t.statusHint3 }}</span>
            <span class="status-hint">{{ t.statusHint4 }}</span>
            <span class="status-hint">{{ t.statusHint5 }}</span>
            <span class="status-hint">{{ t.statusHint6 }}</span>
            <span class="status-hint">{{ t.statusHint7 }}</span>
            <span class="status-hint">{{ t.statusHint8 }}</span>
            <span class="status-counts">
              <span class="count-item">{{ t.statusStaged }}</span> ·
              <span class="count-item">{{ t.statusModified }}</span> ·
              <span class="count-item orange-text">{{ t.statusUntracked }}</span>
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section class="features" id="features">
      <div class="section-header">
        <span class="section-tag">{{ t.featuresTag }}</span>
        <h2>{{ t.featuresTitle }}</h2>
      </div>
      <div class="features-grid">
        <div class="feature-card">
          <div class="feature-icon">◈</div>
          <h3>{{ t.feature1Title }}</h3>
          <p v-html="t.feature1Desc"></p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">⌨</div>
          <h3>{{ t.feature2Title }}</h3>
          <p v-html="t.feature2Desc"></p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">⎇</div>
          <h3>{{ t.feature3Title }}</h3>
          <p v-html="t.feature3Desc"></p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">◉</div>
          <h3>{{ t.feature4Title }}</h3>
          <p v-html="t.feature4Desc"></p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">⚡</div>
          <h3>{{ t.feature5Title }}</h3>
          <p v-html="t.feature5Desc"></p>
        </div>
        <div class="feature-card">
          <div class="feature-icon">🖥</div>
          <h3>{{ t.feature6Title }}</h3>
          <p v-html="t.feature6Desc"></p>
        </div>
      </div>
    </section>

    <!-- Demo Section -->
    <section class="demo-section" id="demo">
      <div class="section-header">
        <span class="section-tag">{{ t.demoTag }}</span>
        <h2>{{ t.demoTitle }}</h2>
      </div>
      <div class="keybindings-showcase">
        <div class="keybind-group">
          <div class="keybind-group-title">{{ t.navGroup }}</div>
          <div class="keybind-item">
            <kbd>j</kbd><kbd>k</kbd>
            <span>{{ t.navUp }} / {{ t.navDown }}</span>
          </div>
          <div class="keybind-item">
            <kbd>Tab</kbd>
            <span>{{ t.navFocus }}</span>
          </div>
          <div class="keybind-item">
            <kbd>1</kbd><kbd>2</kbd>
            <span>{{ t.navTabs }}</span>
          </div>
        </div>
        <div class="keybind-group">
          <div class="keybind-group-title">{{ t.stagingGroup }}</div>
          <div class="keybind-item">
            <kbd>s</kbd>
            <span>{{ t.stageFile }}</span>
          </div>
          <div class="keybind-item">
            <kbd>u</kbd>
            <span>{{ t.unstageFile }}</span>
          </div>
          <div class="keybind-item">
            <kbd>g</kbd>
            <span>{{ t.openMenu }}</span>
          </div>
        </div>
        <div class="keybind-group">
          <div class="keybind-group-title">{{ t.generalGroup }}</div>
          <div class="keybind-item">
            <kbd>r</kbd>
            <span>{{ t.refresh }}</span>
          </div>
          <div class="keybind-item">
            <kbd>q</kbd>
            <span>{{ t.quit }}</span>
          </div>
          <div class="keybind-item">
            <kbd>?</kbd>
            <span>{{ t.help }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Install Section -->
    <section class="install-section" id="install">
      <div class="section-header">
        <span class="section-tag">{{ t.installTag }}</span>
        <h2>{{ t.installTitle }}</h2>
      </div>
      <p class="install-subtitle">
        {{ t.installSubtitle1 }}<br />
        {{ t.installSubtitle2 }}
      </p>

      <div class="install-columns">
        <!-- npm column -->
        <div class="install-col">
          <div class="install-col-header">
            <span class="install-col-badge recommended">{{ t.installNpmBadge }}</span>
            <h3 class="install-col-title">{{ t.installNpmTitle }}</h3>
          </div>
          <div class="install-terminal">
            <div class="install-block">
              <div class="install-comment">{{ t.installRunComment }}</div>
              <div class="install-line">
                <span class="prompt">$</span>
                <span class="command-text"> npx @seen-tui/cli</span>
              </div>
            </div>
            <div class="install-divider"></div>
            <div class="install-block">
              <div class="install-comment">{{ t.installGlobalComment }}</div>
              <div class="install-line">
                <span class="prompt">$</span>
                <span class="command-text"> npm install -g @seen-tui/cli</span>
              </div>
              <div class="install-line">
                <span class="prompt">$</span>
                <span class="command-text"> seen</span>
                <span class="cursor-blink">█</span>
              </div>
            </div>
          </div>
        </div>

        <!-- source column -->
        <div class="install-col">
          <div class="install-col-header">
            <span class="install-col-badge">{{ t.installSourceBadge }}</span>
            <h3 class="install-col-title">{{ t.installCargoTitle }}</h3>
          </div>
          <div class="install-terminal">
            <div class="install-block">
              <div class="install-line">
                <span class="prompt">$</span>
                <span class="command-text"> cargo build --release</span>
              </div>
            </div>
            <div class="install-divider"></div>
            <div class="install-block">
              <div class="install-comment">{{ t.installBuildComment }}</div>
              <div class="install-line">
                <span class="prompt">$</span>
                <span class="command-text"> cd your-git-repo</span>
              </div>
              <div class="install-line">
                <span class="prompt">$</span>
                <span class="command-text"> /path/to/seen/target/release/seen</span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <p class="install-note">
        {{ t.installNote }}
      </p>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="footer-content">
        <div class="footer-logo">
          <span class="logo-icon">⎇</span>
          <span class="logo-text">seen</span>
        </div>
        <p class="footer-desc">{{ t.footerDesc }}</p>
        <div class="footer-links">
          <a href="#">{{ t.footerGitHub }}</a>
          <a href="#">{{ t.footerDocs }}</a>
          <a href="#">{{ t.footerChangelog }}</a>
          <a href="#">{{ t.footerLicense }}</a>
        </div>
        <p class="footer-copy">{{ t.footerCopy }}</p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const cmdCopied = ref(false);
const lang = ref('zh');

const t = computed(() => translations[lang.value]);

function copyCmd() {
  navigator.clipboard.writeText('npx @seen-tui/cli');
  cmdCopied.value = true;
  setTimeout(() => { cmdCopied.value = false; }, 2000);
}

function toggleLang() {
  lang.value = lang.value === 'zh' ? 'en' : 'zh';
}

const translations = {
  zh: {
    navFeatures: '功能特性',
    navKey: '快捷键',
    navInstall: '安装',
    navGitHub: 'GitHub',
    heroBadge: '终端界面 · Git 客户端',
    heroTitle1: '为你的 Git 工作流打造的',
    heroTitle2: '精美 TUI',
    heroDesc1: 'seen 是一个快速、键盘驱动的 Git 终端用户界面。',
    heroDesc2: '浏览文件、查看差异、暂存更改 — 无需离开终端。',
    copyBtn: '复制',
    copiedBtn: '已复制',
    runCmd: '运行命令',
    metaRust: 'Rust 编写',
    metaPlatform: '跨平台',
    metaLicense: 'MIT 许可',
    terminalTitle: 'seen — ~/my-repo — git: master',
    tabGit: 'Git',
    tabGraph: '图表',
    panelFiles: '文件 [focus]',
    panelUntracked: '未追踪 (4)',
    diffUntracked: 'Untracked file：.gitignore',
    diffMuted: 'Stage it first if you want to inspect a patch here.',
    statusHint1: 'g 操作',
    statusHint2: 'r 刷新',
    statusHint3: 's 暂存',
    statusHint4: 'u 取消暂存',
    statusHint5: 'Tab 聚焦',
    statusHint6: 'j/k 导航',
    statusHint7: '1/2 标签',
    statusHint8: 'q 退出',
    statusStaged: '0 已暂存',
    statusModified: '0 已修改',
    statusUntracked: '4 未追踪',
    featuresTag: '$ seen --features',
    featuresTitle: '你需要的一切，不多不少',
    feature1Title: '双面板布局',
    feature1Desc: '左侧文件树，右侧差异查看器。以清晰、密集的布局浏览仓库。',
    feature2Title: '键盘优先',
    feature2Desc: '所有操作都可通过直观的快捷键完成。<code>j/k</code> 导航，<code>s</code> 暂存，<code>Tab</code> 切换面板。',
    feature3Title: '分支和图表视图',
    feature3Desc: '一键切换 Git 状态和提交图表。在终端中可视化你的历史记录。',
    feature4Title: '智能状态追踪',
    feature4Desc: '即时查看已暂存、未暂存和未追踪的文件，带有颜色编码指示器。随时了解仓库状态。',
    feature5Title: '极速性能',
    feature5Desc: '使用 Rust 构建，即使在数千个文件的仓库中也能快速启动和流畅滚动。',
    feature6Title: '跨平台',
    feature6Desc: '支持 macOS、Linux 和 Windows。与现有的终端模拟器和 shell 设置自然集成。',
    demoTag: '$ seen --key',
    demoTitle: '快捷键',
    navGroup: '导航',
    navUp: '上移',
    navDown: '下移',
    navFocus: '切换面板',
    navTabs: '切换标签（Git / 图表）',
    stagingGroup: '暂存',
    stageFile: '暂存文件',
    unstageFile: '取消暂存文件',
    openMenu: '打开操作菜单',
    generalGroup: '常规',
    refresh: '刷新',
    quit: '退出',
    help: '显示帮助',
    installTag: '$ seen --install',
    installTitle: '快速开始',
    installSubtitle1: 'npm 会自动选择正确的原生二进制文件。',
    installSubtitle2: '支持：macOS (arm64, x64) · Linux (arm64, x64) · Windows (x64)',
    installNpmBadge: '推荐',
    installNpmTitle: '通过 npm 安装',
    installRunComment: '# 无需安装直接运行',
    installGlobalComment: '# 或全局安装',
    installSourceBadge: '源码',
    installCargoTitle: '使用 Cargo 构建',
    installBuildComment: '# 在任何 git 仓库内运行：',
    installNote: 'seen 可在任何地方运行。在非 git 仓库中，Git 和图表标签会显示"不是 git 仓库"占位符；文件标签仍可浏览当前目录。',
    footerDesc: '为热爱命令行的开发者打造的终端 Git 界面。',
    footerGitHub: 'GitHub',
    footerDocs: '文档',
    footerChangelog: '更新日志',
    footerLicense: '许可证',
    footerCopy: 'MIT 许可 · 使用 Rust 构建 · 为终端而生'
  },
  en: {
    navFeatures: 'Features',
    navKey: 'Key',
    navInstall: 'Install',
    navGitHub: 'GitHub',
    heroBadge: 'Terminal UI · Git Client',
    heroTitle1: 'A beautiful',
    heroTitle2: 'for your Git workflow',
    highlight: 'TUI',
    heroDesc1: 'seen is a fast, keyboard-driven terminal user interface for Git.',
    heroDesc2: 'Browse files, inspect diffs, stage changes — all without leaving your terminal.',
    copyBtn: 'COPY',
    copiedBtn: 'COPIED',
    runCmd: 'Run command',
    metaRust: 'Written in Rust',
    metaPlatform: 'Cross-platform',
    metaLicense: 'MIT License',
    terminalTitle: 'seen — ~/my-repo — git: master',
    tabGit: 'Git',
    tabGraph: 'Graph',
    panelFiles: 'Files [focus]',
    panelUntracked: 'UNTRACKED (4)',
    diffUntracked: 'Untracked file: .gitignore',
    diffMuted: 'Stage it first if you want to inspect a patch here.',
    statusHint1: 'g actions',
    statusHint2: 'r refresh',
    statusHint3: 's stage',
    statusHint4: 'u unstage',
    statusHint5: 'Tab focus',
    statusHint6: 'j/k nav',
    statusHint7: '1/2 tabs',
    statusHint8: 'q quit',
    statusStaged: '0 staged',
    statusModified: '0 modified',
    statusUntracked: '4 untracked',
    featuresTag: '$ seen --features',
    featuresTitle: 'Everything you need, nothing you don\'t',
    feature1Title: 'Dual-Panel Layout',
    feature1Desc: 'File tree on the left, diff viewer on the right. Navigate your repo at a glance with a clean, information-dense layout.',
    feature2Title: 'Keyboard-First',
    feature2Desc: 'Every action accessible via intuitive keybindings. <code>j/k</code> to navigate, <code>s</code> to stage, <code>Tab</code> to switch focus.',
    feature3Title: 'Branch & Graph View',
    feature3Desc: 'Switch between Git status and commit graph with a single keypress. Visualize your history without leaving the terminal.',
    feature4Title: 'Smart Status Tracking',
    feature4Desc: 'Instantly see staged, modified, and untracked files with color-coded indicators. Always know the state of your repo.',
    feature5Title: 'Blazing Fast',
    feature5Desc: 'Built with Rust for near-instant startup and smooth scrolling even in repositories with thousands of files.',
    feature6Title: 'Cross-Platform',
    feature6Desc: 'Works on macOS, Linux, and Windows. Integrates naturally with your existing terminal emulator and shell setup.',
    demoTag: '$ seen --key',
    demoTitle: 'See it in action',
    navGroup: 'Navigation',
    navUp: 'Move up',
    navDown: 'Move down',
    navFocus: 'Switch focus panel',
    navTabs: 'Switch tabs (Git / Graph)',
    stagingGroup: 'Staging',
    stageFile: 'Stage file',
    unstageFile: 'Unstage file',
    openMenu: 'Open actions menu',
    generalGroup: 'General',
    refresh: 'Refresh',
    quit: 'Quit',
    help: 'Show help',
    installTag: '$ seen --install',
    installTitle: 'Get started in seconds',
    installSubtitle1: 'npm picks the right native binary automatically.',
    installSubtitle2: 'Supported: macOS (arm64, x64) · Linux (arm64, x64) · Windows (x64)',
    installNpmBadge: 'recommended',
    installNpmTitle: 'Via npm',
    installRunComment: '# Run without installing',
    installGlobalComment: '# Or install globally',
    installSourceBadge: 'from source',
    installCargoTitle: 'Build with Cargo',
    installBuildComment: '# Run from inside any git repo:',
    installNote: 'seen runs anywhere. Outside a git repo, the Git and Graph tabs show a "Not a git repository" placeholder; the Files tab still browses the current directory.',
    footerDesc: 'A terminal-native Git interface built for developers who live in the command line.',
    footerGitHub: 'GitHub',
    footerDocs: 'Documentation',
    footerChangelog: 'Changelog',
    footerLicense: 'License',
    footerCopy: 'MIT License · Built with Rust · Made for terminals'
  }
};
</script>

<style scoped>
/* ===== Base ===== */
* {
  box-sizing: border-box;
}

.landing-page {
  min-height: 100vh;
  background: #0d0d0d;
  color: #c9d1d9;
  font-family: 'JetBrains Mono', 'Fira Code', 'Cascadia Code', monospace;
}

/* ===== Navbar ===== */
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 60px;
  height: 60px;
  border-bottom: 1px solid #21262d;
  position: sticky;
  top: 0;
  background: rgba(13, 13, 13, 0.9);
  backdrop-filter: blur(8px);
  z-index: 100;
}

.nav-logo {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 1.1rem;
  font-weight: 700;
  color: #f0f6fc;
}

.logo-icon {
  color: #ff7b72;
  font-size: 1.3rem;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 28px;
}

.lang-toggle {
  border: 1px solid #30363d;
  border-radius: 6px;
  color: #f0f6fc;
  font-family: inherit;
  font-size: 0.75rem;
  padding: 4px 10px;
  cursor: pointer;
  transition: all 0.2s;
  font-weight: 600;
}

.lang-toggle:hover {
  border-color: #ff7b72;
}

.nav-links a {
  color: #8b949e;
  text-decoration: none;
  font-size: 0.875rem;
  transition: color 0.2s;
}

.nav-links a:hover {
  color: #f0f6fc;
}

.github-link {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 6px 14px;
  border-radius: 6px;
  border: 1px solid #30363d;
  color: #f0f6fc !important;
  transition: background 0.2s !important;
}

.github-link:hover {
  background: #30363d !important;
}

/* ===== Hero ===== */
.hero {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 60px;
  padding: 100px 60px;
  max-width: 1280px;
  margin: 0 auto;
}

.hero-content {
  flex: 1;
  max-width: 520px;
}

.badge {
  display: inline-block;
  background: rgba(255, 123, 114, 0.1);
  color: #ff7b72;
  border: 1px solid rgba(255, 123, 114, 0.3);
  border-radius: 20px;
  padding: 4px 14px;
  font-size: 0.75rem;
  margin-bottom: 24px;
  letter-spacing: 0.05em;
}

.hero-title {
  font-size: 3rem;
  font-weight: 800;
  line-height: 1.15;
  color: #f0f6fc;
  margin: 0 0 20px;
}

.highlight {
  color: #ff7b72;
  position: relative;
}

.hero-desc {
  font-size: 1rem;
  line-height: 1.7;
  color: #8b949e;
  margin: 0 0 36px;
}

.hero-actions {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 32px;
  flex-wrap: wrap;
}

/* command pill */
.hero-cmd {
  display: flex;
  align-items: center;
  gap: 10px;
  background: #161b22;
  border: 1px solid #30363d;
  border-radius: 8px;
  padding: 10px 6px 10px 16px;
  font-size: 0.9rem;
}

.hero-cmd-prompt {
  color: #ff7b72;
  font-weight: 700;
  flex-shrink: 0;
}

.hero-cmd-text {
  color: #f0f6fc;
  white-space: nowrap;
}

.hero-cmd-copy {
  background: #21262d;
  border: 1px solid #30363d;
  border-radius: 5px;
  color: #8b949e;
  font-family: inherit;
  font-size: 0.7rem;
  letter-spacing: 0.06em;
  padding: 4px 10px;
  cursor: pointer;
  transition: color 0.15s, border-color 0.15s, background 0.15s;
  flex-shrink: 0;
}

.hero-cmd-copy:hover {
  color: #f0f6fc;
  border-color: #8b949e;
}

.hero-cmd-copy.copied {
  color: #3fb950;
  border-color: #3fb950;
  background: rgba(63, 185, 80, 0.08);
}

/* github button */
.hero-github-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: #161b22;
  border: 1px solid #30363d;
  border-radius: 8px;
  padding: 10px 18px;
  color: #f0f6fc;
  font-size: 0.9rem;
  text-decoration: none;
  white-space: nowrap;
  transition: background 0.2s, border-color 0.2s;
}

.hero-github-btn:hover {
  background: #21262d;
  border-color: #8b949e;
}

.hero-meta {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.meta-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: 0.8rem;
  color: #8b949e;
}

.meta-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
}

.meta-dot.green { background: #3fb950; }
.meta-dot.orange { background: #d29922; }
.meta-dot.blue { background: #58a6ff; }

/* ===== Terminal Preview ===== */
.terminal-wrapper {
  flex: 1;
  max-width: 620px;
}

.terminal {
  background: #161b22;
  border-radius: 12px;
  border: 1px solid #30363d;
  overflow: hidden;
  box-shadow: 0 24px 64px rgba(0, 0, 0, 0.6);
  font-size: 0.78rem;
}

.terminal-titlebar {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 10px 14px;
  background: #1c2128;
  border-bottom: 1px solid #30363d;
}

.terminal-title {
  margin-left: 8px;
  color: #8b949e;
  font-size: 0.75rem;
}

.dot { width: 12px; height: 12px; border-radius: 50%; background-color:#484f58; }

.terminal-tabs {
  display: flex;
  background: #1c2128;
  border-bottom: 1px solid #30363d;
  padding: 0 14px;
}

.tab {
  padding: 6px 14px;
  font-size: 0.75rem;
  color: #8b949e;
  cursor: pointer;
}

.tab.active {
  color: #f0f6fc;
  border-bottom: 2px solid #ff7b72;
}

.terminal-body {
  display: flex;
  min-height: 180px;
}

.panel-left {
  width: 200px;
  padding: 10px 0;
  border-right: 1px solid #30363d;
  flex-shrink: 0;
}

.panel-header {
  padding: 2px 14px;
  color: #f0f6fc;
  font-size: 0.75rem;
  margin-bottom: 4px;
}

.panel-subheader {
  padding: 2px 14px;
  font-size: 0.7rem;
  margin-bottom: 4px;
}

.panel-subheader.untracked {
  color: #d29922;
}

.file-item {
  padding: 3px 14px;
  font-size: 0.72rem;
  color: #3fb950;
  cursor: pointer;
}

.active-file {
  background: rgba(255, 123, 114, 0.15);
  color: #ff7b72;
}

.panel-divider {
  width: 1px;
  background: #30363d;
}

.panel-right {
  flex: 1;
  padding: 10px 14px;
}

.diff-line {
  display: flex;
  gap: 8px;
  align-items: center;
  margin-bottom: 8px;
}

.diff-filename {
  color: #f0f6fc;
  font-size: 0.75rem;
}

.diff-tag {
  color: #8b949e;
  font-size: 0.72rem;
}

.diff-info {
  font-size: 0.72rem;
  color: #8b949e;
  line-height: 1.6;
}

.diff-info.muted {
  color: #484f58;
}

.terminal-statusbar {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 8px 14px;
  background: #1c2128;
  border-top: 1px solid #30363d;
  flex-wrap: wrap;
}

.status-hint {
  font-size: 0.68rem;
  color: #484f58;
}

.status-counts {
  margin-left: auto;
  font-size: 0.68rem;
  color: #484f58;
  display: flex;
  align-items: center;
  gap: 4px;
}

.count-item { color: #484f58; }
.orange-text { color: #d29922; }

/* ===== Sections Common ===== */
.section-header {
  text-align: center;
  margin-bottom: 56px;
}

.section-tag {
  display: inline-block;
  color: #3fb950;
  font-size: 0.85rem;
  margin-bottom: 14px;
}

.section-header h2 {
  font-size: 2rem;
  font-weight: 700;
  color: #f0f6fc;
  margin: 0;
}

/* ===== Features ===== */
.features {
  padding: 100px 60px;
  max-width: 1280px;
  margin: 0 auto;
}

.features-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.feature-card {
  background: #161b22;
  border: 1px solid #21262d;
  border-radius: 12px;
  padding: 28px;
  transition: border-color 0.2s, transform 0.2s;
}

.feature-card:hover {
  border-color: #ff7b72;
  transform: translateY(-2px);
}

.feature-icon {
  font-size: 1.6rem;
  margin-bottom: 14px;
  color: #ff7b72;
}

.feature-card h3 {
  font-size: 1rem;
  font-weight: 700;
  color: #f0f6fc;
  margin: 0 0 10px;
}

.feature-card p {
  font-size: 0.85rem;
  color: #8b949e;
  line-height: 1.7;
  margin: 0;
}

.feature-card code {
  background: #21262d;
  padding: 1px 5px;
  border-radius: 4px;
  color: #ff7b72;
  font-size: 0.82rem;
}

/* ===== Demo / Keybindings ===== */
.demo-section {
  padding: 100px 60px;
  background: #0a0a0a;
}

.keybindings-showcase {
  display: flex;
  justify-content: center;
  gap: 60px;
  max-width: 900px;
  margin: 0 auto;
}

.keybind-group {
  flex: 1;
}

.keybind-group-title {
  font-size: 0.75rem;
  color: #8b949e;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  margin-bottom: 16px;
  padding-bottom: 8px;
  border-bottom: 1px solid #21262d;
}

.keybind-item {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 14px;
  font-size: 0.85rem;
  color: #8b949e;
}

kbd {
  display: inline-block;
  background: #21262d;
  border: 1px solid #30363d;
  border-radius: 4px;
  padding: 2px 8px;
  font-size: 0.78rem;
  color: #f0f6fc;
  font-family: inherit;
  min-width: 28px;
  text-align: center;
}

/* ===== Install ===== */
.install-section {
  padding: 100px 60px;
  max-width: 1100px;
  margin: 0 auto;
}

.install-subtitle {
  text-align: center;
  color: #8b949e;
  font-size: 0.85rem;
  line-height: 1.7;
  margin: -32px 0 56px;
}

.install-columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  margin-bottom: 36px;
}

.install-col-header {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 14px;
}

.install-col-title {
  font-size: 1rem;
  font-weight: 700;
  color: #f0f6fc;
  margin: 0;
}

.install-col-badge {
  display: inline-block;
  font-size: 0.7rem;
  padding: 2px 10px;
  border-radius: 20px;
  border: 1px solid #30363d;
  color: #8b949e;
  letter-spacing: 0.04em;
}

.install-col-badge.recommended {
  background: rgba(255, 123, 114, 0.1);
  border-color: rgba(255, 123, 114, 0.35);
  color: #ff7b72;
}

/* terminal window shared with hero */
.install-terminal {
  background: #161b22;
  border: 1px solid #30363d;
  border-radius: 12px;
  overflow: hidden;
  font-size: 0.82rem;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.4);
}

.install-terminal-bar {
  display: flex;
  align-items: center;
  gap: 6px;
  padding: 10px 14px;
  background: #1c2128;
  border-bottom: 1px solid #30363d;
}

.install-block {
  padding: 16px 20px;
}

.install-divider {
  height: 1px;
  background: #21262d;
  margin: 0 20px;
}

.install-comment {
  color: #484f58;
  font-size: 0.78rem;
  margin-bottom: 6px;
}

.install-line {
  display: flex;
  align-items: center;
  gap: 10px;
  line-height: 1.9;
}

.prompt {
  color: #3fb950;
  font-weight: 700;
  flex-shrink: 0;
}

.command-text {
  color: #f0f6fc;
}

.cursor-blink {
  color: #f0f6fc;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.install-note {
  text-align: center;
  color: #484f58;
  font-size: 0.8rem;
  line-height: 1.7;
  margin: 0;
  padding: 20px 24px;
  border: 1px solid #21262d;
  border-radius: 8px;
  background: #0a0a0a;
}

/* ===== Footer ===== */
.footer {
  border-top: 1px solid #21262d;
  padding: 60px;
  text-align: center;
}

.footer-logo {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-size: 1.1rem;
  font-weight: 700;
  color: #f0f6fc;
  margin-bottom: 14px;
}

.footer-desc {
  color: #8b949e;
  font-size: 0.85rem;
  margin: 0 0 24px;
}

.footer-links {
  display: flex;
  justify-content: center;
  gap: 24px;
  margin-bottom: 24px;
}

.footer-links a {
  color: #8b949e;
  text-decoration: none;
  font-size: 0.85rem;
  transition: color 0.2s;
}

.footer-links a:hover {
  color: #f0f6fc;
}

.footer-copy {
  color: #484f58;
  font-size: 0.75rem;
  margin: 0;
}

/* ===== Responsive ===== */
@media (max-width: 1024px) {
  .hero {
    flex-direction: column;
    padding: 60px 24px;
  }

  .hero-content {
    max-width: 100%;
    text-align: center;
  }

  .hero-actions {
    justify-content: center;
  }

  .hero-meta {
    justify-content: center;
  }

  .terminal-wrapper {
    max-width: 100%;
    width: 100%;
  }

  .features-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .navbar {
    padding: 0 24px;
  }

  .features,
  .install-section {
    padding: 60px 24px;
  }

  .demo-section {
    padding: 60px 24px;
  }
}

@media (max-width: 640px) {
  .features-grid {
    grid-template-columns: 1fr;
  }

  .keybindings-showcase {
    flex-direction: column;
    gap: 32px;
  }

  .hero-title {
    font-size: 2rem;
  }

  .nav-links a:not(.github-link) {
    display: none;
  }

  .install-columns {
    grid-template-columns: 1fr;
  }
}
</style>
