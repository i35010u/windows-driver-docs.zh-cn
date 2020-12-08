---
title: GFlags 详细信息
description: GFlags 详细信息
keywords:
- GFlags，详细信息
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4fbc8e2adf10eaf81b1f6533db903a56192fe65a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834745"
---
# <a name="gflags-details"></a>GFlags 详细信息

GFlags 通过编辑 Windows 注册表和内部设置来启用和禁用系统功能。 本部分详细说明了 GFlags 的操作，并提供了使用 GFlags 最有效的提示。

## <a name="general-information"></a>常规信息

- 若要显示 "GFlags" 对话框，请在命令行中键入 " **GFlags** (没有参数) 。

- GFlags 系统级注册表设置会立即显示在注册表中，但在重新启动系统之前，不会生效。

- GFlags 映像文件会立即显示在注册表中，但在重新启动该过程之前，不会生效。

- "GFlags" 对话框中的 "调试器" 和 "启动" 功能是特定于程序的。 一次只能对一个图像文件设置它们。

### <a name="flag-details"></a>标记详细信息

- 若要清除所有标志，请将标志设置为-FFFFFFFF。 将标志设置为0会将0添加到当前标志值。

- 将图像文件的标志设置为 FFFFFFFF (0xFFFFFFFF) 时，Windows 将清除映像文件的所有标志，并删除映像文件注册表项中的 **GlobalFlag** 条目。 将保留映像文件注册表项。

### <a name="dialog-box-and-command-line"></a>对话框和命令行

可以通过使用其便捷对话框或从命令行运行 GFlags。 大多数功能都可用于这两种形式，但以下情况例外。

#### <a name="dialog-box-only"></a>仅对话框

- 开始. 使用指定的标志启动程序。

- 在调试器中运行程序。

- Windows Vista 之前的系统上的[特殊池](special-pool.md)。 在 Windows Vista 和更高版本的 Windows 上，你可以在命令行或在 Gflags 对话框中配置特殊池功能。

#### <a name="command-line-only"></a>仅命令行

-  (/tracedb) 设置用户模式堆栈跟踪数据库的大小。

- 设置页堆验证选项。

### <a name="registry-information"></a>注册表信息

在会话之间保存的 GFlags 设置存储在注册表中。 您可以使用注册表 Api、Regedit 或 reg.exe 来查询或更改这些值。 下表列出了设置的类型以及它们在注册表中的存储位置。

|设置的类型|注册表位置|
|----|----|
|系统范围设置 ( "注册表" ) |HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\\ **GlobalFlag**|
|对于计算机的所有用户， ( "映像文件" ) ，特定于程序的设置。|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\ *ImageFileName* \\ **GlobalFlag**|
|对于该计算机的所有用户，特定程序的无提示退出设置 ( "无提示进程退出" ) 。|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\\ * *_ImageFileName_* _|
|计算机所有用户的图像文件的页面堆选项|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\\ _ImageFileName *\\ * * PageHeapFlags**
|用户模式堆栈跟踪数据库大小 (**tracedb**) |HKLM\SOFTWARE\Microsoft\Windows nt\currentversion\image file execution 文件执行选项 \\ *ImageFileName* \\ **StackTraceDatabaseSizeInMb**|
|为映像文件创建用户模式堆栈跟踪数据库 (ust，0x1000) |Windows 会将图像文件名称添加到 USTEnabled 注册表项的值 (HKLM\SOFTWARE\Microsoft\Windows Nt\currentversion\image file execution File 执行 Options \\ **USTEnabled**) 。
|在可能的情况下大型页加载映像|HKLM\SOFTWARE\Microsoft\Windows nt\currentversion\image file execution 文件执行选项 \\ *ImageFileName* \\ **UseLargePages**。
|特殊池 (内核特殊池标记) |HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management \\ **PoolTag**|
验证开始/验证结束|HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\PoolTagOverruns。 " **验证启动** " 选项将值设置为0。 **验证结束** 选项将值设置为1。
|映像文件的调试器|HKLM\SOFTWARE\Microsoft\Windows nt\currentversion\image file execution 文件执行选项 \\ *ImageFileName* \\ **调试器**
|对象引用跟踪|HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Kernel \\ **ObTraceProcessName**、 **ObTracePermanent** 和 **ObTracePoolTags**
