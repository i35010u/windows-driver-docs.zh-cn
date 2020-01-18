---
title: WinDbg 预览-键盘快捷方式
description: 本部分提供 WinDbg 预览调试器的键盘快捷方式。
ms.date: 01/09/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7fc4e7cec30ea3d6ed032ccdc9f12a5ee991117b
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256746"
---
# <a name="windbg-preview-keyboard-shortcuts"></a>WinDbg 预览键盘快捷方式

![windbg 预览版上的小徽标](images/windbgx-preview-logo.png)

本部分总结了 WinDbg 预览调试器的键盘快捷方式。

所有功能区菜单选项都可使用**Alt +** 选项的第一个字母。 例如，按**alt + h**以切换到 "主页" 菜单，按**alt + h + S**停止调试。

![主菜单的屏幕截图，其中显示了用于功能区的快捷键](images/windbgx-ribbon-home-menu-alt-keys.png)

### <a name="flow-control"></a>Flow control

| 击键     | 描述             |
| ------------- |-------------------------|
 F5 | “继续”
F10     | 单步跳过
F11     | 步入
Shift+F11   |   单步跳出
F7      | 运行到行
Ctrl+Shift+I    |   将指令指针设置为突出显示的行
Ctrl + Break 或 Alt + Del   |   会间休息
Ctrl+Shift+F5   |   “重启”
Shift+F5    |   停止调试
Alt + H、D     | 分离

### <a name="setup"></a>“安装程序”

| 击键     | 描述             |
| ------------- |-------------------------|
F6      |   附加到进程
Ctrl+R      |       连接到远程
Ctrl+D      |       打开转储文件
Ctrl+K      |       附加到内核调试器
Ctrl+E      |       启动进程
Ctrl+P      |       启动应用程序包

### <a name="breakpoints"></a>断点

| 击键     | 描述             |
| ------------- |-------------------------|  
F9          |  在突出显示的行上切换断点
Ctrl+Alt+K      |   切换初始断点
Alt + B，A         |  添加断点

### <a name="windowing"></a>窗口化

| 击键     | 描述             |
| ------------- |-------------------------|
Ctrl+Tab        |       打开窗口变换器
Ctrl+1      |       打开/专注于命令窗口
Ctrl+2      |       打开/专注于监视窗口
Ctrl+3      |       打开/专注于 "局部变量" 窗口
Ctrl+4      |       打开/专注于 "寄存器" 窗口
Ctrl+5      |       打开/关注内存窗口
Ctrl+6      |       打开/专注于堆栈窗口
Ctrl+7      |       打开/专注于反汇编窗口
Ctrl+8      |       打开/专注于 "断点" 窗口
Ctrl+9      |       在线程窗口上打开/焦点

### <a name="scripting"></a>编写脚本

| 击键      | 描述             |
| -------------- |-------------------------|
Ctrl+Shift+O     |      打开脚本
Ctrl+Shift+Enter |      执行脚本
Ctrl+S           |      保存脚本
Alt + S、N          |      新脚本
Alt + S、U          |      取消链接脚本

### <a name="stack-navigation"></a>堆栈导航

| 击键     | 描述             |
| ------------- |-------------------------|
Ctrl+↑ / ↓      |   在堆栈帧中上移/下移

### <a name="help"></a>Help

| 击键     | 描述             |
| ------------- |-------------------------|
F1              |       打开帮助文件
Shift+F1        |       联机搜索选择（源窗口）

### <a name="misc"></a>杂项  

| 击键     | 描述             |
| ------------- |-------------------------|
Ctrl+Alt+V      |       切换详细模式

## <a name="see-also"></a>另请参阅

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)
