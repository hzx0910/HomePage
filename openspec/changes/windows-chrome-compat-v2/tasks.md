## 1. CSS 静态 Fallback

- [x] 1.1 将 `:root` 中四个 `color-mix()` 变量替换为默认主题色的精确计算等价值：`--surface: rgba(20,25,40,1)`、`--surface2: rgba(26,33,56,1)`、`--border: rgba(30,39,68,0.532)`、`--modal-bg: rgba(15,21,35,0.871)`
- [x] 1.2 移除 `body.has-bg` 规则中 `--surface` 和 `--surface2` 的 `color-mix()` 覆盖行（保留 `--accent` 和 `--accent-hover` 的覆盖）

## 2. JS 混色计算

- [x] 2.1 在 `Settings.applyAccent()` 末尾添加 `mix(base, accent, t)` 线性插值函数和 alpha 计算逻辑
- [x] 2.2 检测 `body.has-bg`，有背景图时 surface alpha 用 `0.12*1 + 0.88*0.3 = 0.384`，无背景图时用 `1`
- [x] 2.3 计算并 setProperty 四个派生变量：`--surface`、`--surface2`、`--border`（alpha=`0.22*1+0.78*0.4=0.532`）、`--modal-bg`（alpha=`0.14*1+0.86*0.85=0.871`）

## 3. 背景图联动

- [x] 3.1 修改 `Settings._applyBackground()`：`classList.add('has-bg')` 后调用 `applyAccent()` 更新 surface 透明度
- [x] 3.2 修改 `Settings._removeBackground()`：`classList.remove('has-bg')` 后调用 `applyAccent()` 恢复 surface 不透明

## 4. 验证

- [ ] 4.1 macOS Chrome：无背景图时模块背景和边框正常显示，颜色与原版一致
- [ ] 4.2 macOS Chrome：切换主题色后 surface/border 颜色同步更新
- [ ] 4.3 macOS Chrome：设置背景图后模块半透明可透出背景
- [ ] 4.4 macOS Chrome：移除背景图后模块恢复不透明
- [ ] 4.5 Windows Chrome：无背景图时模块背景和边框正常显示（核心修复）
