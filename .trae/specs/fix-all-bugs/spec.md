# 修复已知 Bug 和异常处理 Spec

## Why
应用程序在关键位置吞噬了异常或缺乏适当的错误处理，导致 silent failures（静默失败）和潜在的应用程序崩溃。此外，`LogHelper` 中的异常日志记录方法是空的，使得调试变得困难。

## What Changes
- **修复日志记录**: 实现 `LogHelper.NewLog(Exception ex)` 以将异常详细信息写入日志文件。
- **添加错误处理**:
    - 在 `MW_Screenshot.cs` 中的 `SaveScreenShotToDesktop` 方法添加 `try-catch` 块，以处理文件保存失败并向用户显示提示。
    - 在 `FullscreenSnapshot` 中处理 `NotSupportedException`，记录警告而不是直接吞噬。
    - 在 `MW_AutoStart.cs` 中的 `StartAutomaticallyCreate` 和 `StartAutomaticallyDel` 方法的 `catch` 块中添加日志记录。
    - 在 `ScreenshotWindow.xaml.cs` 的 `IconMouseUp` 事件处理程序中添加 `try-catch` 块，防止异步操作失败导致应用崩溃。

## Impact
- **Affected specs**: 错误处理和日志记录机制。
- **Affected code**:
    - `InkCanvasForClass/Helpers/LogHelper.cs`
    - `InkCanvasForClass/MainWindow_cs/MW_Screenshot.cs`
    - `InkCanvasForClass/MainWindow_cs/MW_AutoStart.cs`
    - `InkCanvasForClass/Popups/ScreenshotWindow.xaml.cs`

## ADDED Requirements
### Requirement: 异常日志记录
系统 SHALL 将捕获的异常详细信息写入日志文件，而不是忽略它们。

#### Scenario: 异常发生
- **WHEN** 发生异常（如文件保存失败、权限不足等）
- **THEN** 异常信息及其堆栈跟踪应被记录到 `Log.txt` 文件中。
- **THEN** 如果适用，应向用户显示 Toast 通知说明错误。

## MODIFIED Requirements
### Requirement: 截图保存错误处理
在保存截图到桌面或剪贴板时，如果操作失败，系统 SHALL 捕获异常并通知用户。

### Requirement: 开机自启设置错误处理
在设置或取消开机自启时，如果操作失败，系统 SHALL 记录错误，而不是静默失败。
