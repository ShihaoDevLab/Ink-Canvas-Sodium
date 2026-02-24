# 修复全屏截图保存崩溃与扩展名不一致 Spec

## Why
当前全屏截图保存逻辑在未显式配置保存目录时可能触发空引用崩溃；同时输出格式与文件名扩展名可能不一致，导致用户误判文件格式或无法正确打开。

## What Changes
- FullscreenSnapshot 在 IsSaveToLocal=true 且 BitmapSavePath 为空时使用默认目录（桌面）而不是崩溃
- 保存文件名扩展名自动与 OutputMIMEType 对齐；若模板未包含扩展名则自动追加
- SaveBitmapFileName 为空或空白时回退到默认模板

## Impact
- Affected specs: 截图保存到本地、截图输出格式、截图文件命名模板
- Affected code: inkcanvasforclass/mainwindow_cs/MW_Screenshot.cs

## ADDED Requirements
### Requirement: 保存目录默认值
系统 SHALL 在保存截图到本地时保证存在有效的保存目录。

#### Scenario: Success case
- **WHEN** 调用 FullscreenSnapshot 且 IsSaveToLocal=true 但 BitmapSavePath 为 null
- **THEN** 使用桌面目录作为保存目录，成功保存图片并返回 Bitmap，不抛出 NullReferenceException

### Requirement: 输出扩展名一致性
系统 SHALL 使最终保存文件扩展名与 OutputMIMEType 一致。

#### Scenario: Success case
- **WHEN** OutputMIMEType=Jpeg 且 SaveBitmapFileName 以 .png 结尾或不包含扩展名
- **THEN** 最终保存文件扩展名为 .jpg 或 .jpeg，且图片实际编码为 Jpeg

## MODIFIED Requirements
### Requirement: 截图失败提示
当截图保存发生异常时，系统 SHALL 保持现有对外错误提示语义（“截图保存失败: …”），但不得因配置缺省而抛出空引用异常。

## REMOVED Requirements
无
