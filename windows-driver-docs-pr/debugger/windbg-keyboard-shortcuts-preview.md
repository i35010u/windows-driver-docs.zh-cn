---
title: WinDbg 预览版-键盘快捷方式
description: 本部分提供有关 WinDbg 预览调试器键盘快捷方式。
ms.date: 08/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ea41f3c3bf56bb02a6be0346199ce9786d0d0d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353140"
---
# <a name="windbg-preview-keyboard-shortcuts"></a>WinDbg 预览键盘快捷方式 

本部分总结了 WinDbg 预览调试器键盘快捷方式。

所有功能区菜单选项都可使用**Alt +** 选项的第一个字母。 例如**Alt + H**转到主页菜单上**Alt + H + P**若要查看帮助。

![显示对功能区快速密钥使用字母的主菜单的屏幕截图](images/windbgx-ribbon-home-menu-alt-keys.png)


### <a name="flow-control"></a>流控制

| 击键     | 描述             |
| ------------- |-------------------------|
 F5 | 继续 
F10     | 逐过程执行 
F11     | 步入
Shift+F11   |   跳出
F7      | 运行到行
Ctrl+Shift+I    |   指令指针设置为突出显示的行
Ctrl + Break 或 Alt + Del   |   会间休息
Ctrl+Shift+F5   |   “重新启动”
Shift+F5    |   停止调试
Alt + H D     | 分离



### <a name="setup"></a>安装

| 击键     | 描述             |
| ------------- |-------------------------|
F6      |   附加到进程
Ctrl+R      |       连接到远程
Ctrl+D      |       打开转储文件
Ctrl+K      |       将附加到内核调试程序
Ctrl+E      |       启动进程
Ctrl+P      |       启动应用包

### <a name="breakpoints"></a>断点         

| 击键     | 描述             |
| ------------- |-------------------------|  
F9          |  突出显示的行上切换断点
Ctrl+Alt+K      |   切换初始中断
Alt+B,A         |  添加断点

### <a name="windowing"></a>窗口化

| 击键     | 描述             |
| ------------- |-------------------------|
Ctrl+Tab        |       打开窗口换带机
Ctrl+1      |       打开/重点在命令窗口
Ctrl+2      |       打开/重点上监视窗口
Ctrl+3      |       打开/焦点在局部变量窗口
Ctrl+4      |       打开/重点上寄存器窗口
Ctrl+5      |       打开/重点上内存窗口
Ctrl+6      |       打开/重点堆栈窗口
Ctrl+7      |       打开/重点在反汇编窗口
Ctrl+8      |       打开/重点上断点窗口
Ctrl+9      |       打开/重点在线程窗口


### <a name="scripting"></a>编写脚本

| 击键      | 描述             |
| -------------- |-------------------------|
Ctrl+Shift+O     |      打开脚本
Ctrl+Shift+Enter |      执行脚本
Ctrl+S           |      保存脚本
Alt+S,N          |      新的脚本
Alt + S、 U          |      取消链接脚本


### <a name="stack-navigation"></a>堆栈导航

| 击键     | 描述             |
| ------------- |-------------------------|
Ctrl + ↑ / ↓      |   上移/下移一个堆栈帧


### <a name="help"></a>Help 

| 击键     | 描述             |
| ------------- |-------------------------|
F1              |       打开帮助文件
Shift+F1        |       联机搜索选择 （源窗口）


### <a name="misc"></a>杂项  

| 击键     | 描述             |
| ------------- |-------------------------|
Ctrl+Alt+V      |       切换详细模式




## <a name="see-also"></a>请参阅

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)






