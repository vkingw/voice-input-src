```bash
claude \
  --dangerously-skip-permissions \
  --output-format=stream-json \
  --verbose \
  -p "请实现一个 macOS menu-bar 语音输入法应用（Swift，macOS 14+），具体要求：

1. 按住 Fn 键录音，松开后将转录文字注入当前聚焦的输入框。优先使用流式转录（Apple Speech Recognition framework）。
2. 默认语言为简体中文（zh-CN），同时在菜单栏提供语言切换选项（英语、简体中文、繁体中文、日语、韩语）。
3. 录音时显示一个无边框胶囊状悬浮窗（高 56px，圆角半径 28px），使用 NSPanel + NSVisualEffectView（.hudWindow 材质），包含：
   - 左侧 5 根竖条波形动画（44×32px），由实时音频 RMS 电平驱动（非随机脉冲），各竖条权重为 [0.5, 0.8, 1.0, 0.75, 0.55] 形成自然的中间高两侧低效果，平滑包络（attack 40%、release 15%），每根竖条添加 ±4% 随机抖动增加有机感
   - 右侧文字标签（弹性宽度 160-560px）实时显示转录文本
   - 入场弹簧动画（0.35s）、文字宽度平滑过渡（0.25s）、退场缩放动画（0.22s）
4. 文字注入使用剪贴板 + 模拟 Cmd+V 粘贴方式，注入前需检测当前输入法：如果是 CJK 输入法，先临时切换到 ASCII 输入源（ABC/US 键盘）再粘贴，粘贴完成后恢复原输入法，防止中文输入法拦截 Cmd+V。注入完成后恢复原剪贴板内容。
5. Fn 键通过 CGEvent tap 全局监听，需抑制 Fn 事件传递以防止触发 emoji 选择器。
6. 应用以 LSUIElement 模式运行（仅菜单栏图标，无 Dock 图标）。语言选择存储在 UserDefaults 中。
7. 使用 Swift Package Manager 构建，提供 Makefile（build/run/install/clean），构建产物为签名的 .app bundle。"
```
