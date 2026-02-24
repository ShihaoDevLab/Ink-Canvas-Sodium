# Tasks
- [x] Task 1: 复现并定位截图保存崩溃
  - [x] 在代码中确认 FullscreenSnapshot 的保存路径/文件名构造路径
  - [x] 构造 IsSaveToLocal=true 且 BitmapSavePath=null 的调用路径用于复现
  - [x] 记录触发点与期望行为对比

- [x] Task 2: 实现保存路径与文件名健壮性修复
  - [x] 为 BitmapSavePath 为空时提供默认目录（桌面）
  - [x] 处理 SaveBitmapFileName 为空/空白回退默认模板
  - [x] 让最终文件扩展名与 OutputMIMEType 对齐（替换或追加）

- [x] Task 3: 验证与回归检查
  - [x] 运行解决方案构建，确保无编译错误
  - [x] 手动验证全屏截图保存（PNG/BMP/JPEG）扩展名与格式一致
  - [x] 验证复制到剪贴板路径不受影响

# Task Dependencies
- Task 2 depends on Task 1
- Task 3 depends on Task 2
