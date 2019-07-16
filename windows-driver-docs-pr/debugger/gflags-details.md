---
title: GFlags 详细信息
description: GFlags 详细信息
ms.assetid: 97faa63d-b876-4973-812f-f3bdd57c1778
keywords:
- GFlags、 详细信息
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 858425dd05b286a6d2584acee7185a8e50828a9b
ms.sourcegitcommit: 707739250ebdcd74a26d85d8b4217fa81c9c9e95
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68181279"
---
# <a name="gflags-details"></a>GFlags 详细信息

GFlags 启用和禁用通过编辑 Windows 注册表和内部设置的系统功能。 本部分介绍 GFlags 的详细信息中的操作，并包括最有效地使用 GFlags 的技巧。

## <a name="general-information"></a>常规信息

- 若要显示 GFlags 对话框中，在命令行处，键入**gflags** （不带任何参数）。

- GFlags 系统级注册表设置在注册表中会立即显示，但直到重新启动系统不会生效。

- GFlags 图像文件注册表设置在注册表中会立即显示，但直到重新启动该进程不会生效。

- GFlags 对话框中的调试器和启动功能是特定的程序。 您可以仅设置其上一个图像文件一次。

### <a name="flag-details"></a>标志的详细信息

- 若要清除所有标志，请将标志设置为-FFFFFFFF。 将标志设置为 0 将 0 添加到当前的标志值。

- Windows 将图像文件的标志设置为 FFFFFFFF (0xFFFFFFFF)，清除所有标志的图像文件，并删除**GlobalFlag**图像文件注册表项中的条目。 保留图像文件注册表项。

### <a name="dialog-box-and-command-line"></a>对话框和命令行

可以通过使用其方便的对话框或命令行运行 GFlags。 大多数功能均可在两种形式，但存在以下例外。

#### <a name="dialog-box-only"></a>仅限对话框

- 启动。 开始使用指定的标志的程序。

- 在调试器中运行程序。

- [特殊池](special-pool.md)Windows Vista 之前的系统上。 在 Windows Vista 和更高版本的 Windows 上，可以在命令行或 Gflags 对话框中配置特殊池功能。

#### <a name="command-line-only"></a>只有命令行

- 设置的用户模式堆栈跟踪数据库大小 (/ tracedb)。

- 设置页面堆验证选项。

### <a name="registry-information"></a>注册表信息

会话之间保存的 GFlags 设置存储在注册表中。 可以使用注册表 Api、 Regedit 中或 reg.exe 来查询或更改这些值。 下表列出了设置和注册表中存储的类型。

|设置类型|注册表位置|
|----|----|
|系统级设置 （"注册表"）|HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\\**GlobalFlag**|
|计算机的所有用户的特定于程序的设置 ("Image file")。|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\*映像文件名*\\**GlobalFlag**|
|计算机的所有用户的特定程序 （"无提示进程退出"） 的无提示退出设置。|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\\***映像文件名***|
|计算机的所有用户的图像文件的页面堆选项|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\*映像文件名*\\**PageHeapFlags**
|用户模式堆栈跟踪数据库大小 (**tracedb**)|HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\*映像文件名*\\**StackTraceDatabaseSizeInMb**|
|创建用户模式堆栈跟踪数据库 (ust，0x1000) 的图像文件|Windows 将图像文件名称添加到 USTEnabled 注册表项的值 (HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\**USTEnabled**)。
|在可能的情况下大型页加载映像|HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\*映像文件名*\\**UseLargePages**。
|特殊池 （内核特殊池标记）|HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\\**PoolTag**|
验证开始/验证结束|HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PoolTagOverruns。 **验证启动**选项设置为 0 的值。 **验证结束**选项的值设置为 1。
|图像文件的调试器|HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\*映像文件名*\\**调试器**
|对象引用跟踪|HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Kernel\\**ObTraceProcessName**， **ObTracePermanent**和**ObTracePoolTags**
