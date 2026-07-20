# Unity UI 设计笔记

## Canvas（画布）
- 所有UI元素的父级容器
- 渲染模式：Screen Space - Overlay / Camera / World Space
- Canvas Scaler：UI自适应缩放

## 核心UI组件

| 组件 | 用途 |
|------|------|
| Button | 按钮交互 |
| Text (TMP) | 文本显示 (TextMeshPro) |
| Image | 图片显示 |
| Slider | 滑动条（进度/调节） |
| Dropdown | 下拉选择 |
| InputField | 文本输入 |
| Toggle | 开关选择 |

## UI交互设计要点
- 按钮点击事件绑定：Inspector面板拖拽 或 代码动态绑定
- 按钮状态：Normal / Highlighted / Pressed / Disabled
- UI动画：通过Animator或DoTween实现
- 反馈设计：点击音效、颜色变化、动画反馈

## TextMeshPro（TMP）
- 推荐代替传统Text组件
- 支持更多字体样式和效果
- 需要导入 TMP Essential Resources

## 本系统UI模块
- 主页菜单UI
- 情绪自评UI（前测/后测）
- 训练引导UI
- 数据记录展示UI
- 设置界面UI
