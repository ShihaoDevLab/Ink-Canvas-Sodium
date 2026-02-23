# Tasks

- [x] Task 1: 修复 `LogHelper` 中的异常记录功能
  - [x] SubTask 1.1: 修改 `LogHelper.NewLog(Exception ex)` 方法，使其调用 `WriteLogToFile` 记录异常信息。
- [x] Task 2: 修复 `MW_Screenshot.cs` 中的错误处理
  - [x] SubTask 2.1: 为 `SaveScreenShotToDesktop` 方法添加 `try-catch` 块，捕获异常并显示错误 Toast。
  - [x] SubTask 2.2: 在 `FullscreenSnapshot` 方法中，当捕获 `NotSupportedException` 时添加日志记录。
- [x] Task 3: 修复 `MW_AutoStart.cs` 中的错误处理
  - [x] SubTask 3.1: 在 `StartAutomaticallyCreate` 的 `catch` 块中添加 `LogHelper.NewLog` 调用。
  - [x] SubTask 3.2: 在 `StartAutomaticallyDel` 的 `catch` 块中添加 `LogHelper.NewLog` 调用。
- [x] Task 4: 修复 `ScreenshotWindow.xaml.cs` 中的异步错误处理
  - [x] SubTask 4.1: 在 `IconMouseUp` 方法中包裹 `await` 调用（如 `GetAllWindowsAsync`）在 `try-catch` 块中，防止崩溃并记录错误。
