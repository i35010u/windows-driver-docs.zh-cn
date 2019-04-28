---
title: 示例 8 扩大用户模式堆栈跟踪数据库
description: 示例 8 扩大用户模式堆栈跟踪数据库
ms.assetid: b04f6b86-a210-4941-a4eb-a9059d9890d9
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b2a72106e22c3737782ceb0b48aca8d5d791971
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344151"
---
# <a name="example-8-enlarging-the-user-mode-stack-trace-database"></a>示例 8：扩大用户模式堆栈跟踪数据库


## <span id="ddk_example_8___enlarging_the_user_mode_stack_trace_database_dtools"></span><span id="DDK_EXAMPLE_8___ENLARGING_THE_USER_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


以下 GFlags 命令会增加用户模式堆栈跟踪数据库中为 myapp.exe，虚构的程序，从为 24 MB 8 MB 的最大大小。

该命令使用 **/i**参数来指定图像文件。 它使用 **/tracedb**参数设置最大堆栈跟踪数据库大小和 24 以指示的大小以兆字节为单位的值。 该命令使用小数单位。 （十六进制的单位是无效的。）

```console
gflags /i MyApp.exe /tracedb 24
```

如以下的错误消息，此命令会失败，因为[创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md)（+ ust） 标志未设置为 MyApp 图像文件。 无法设置跟踪数据库的大小，直到您创建一个。

```console
Failed to set the trace database size for `MyApp.exe'
```

以下命令修复此错误。 第一个命令创建 myapp.exe 跟踪数据库和第二个命令将跟踪数据库的最大大小设置为 24 MB。 这些命令不能合并到单个命令。 以下屏幕将显示从 GFlags 命令和成功消息。

```console
gflags /i MyApp.exe +ust

Current Registry Settings for MyApp.exe executable are: 00001000
    ust - Create user mode stack trace database

gflags /i MyApp.exe /tracedb 24

Trace database size for `MyApp.exe' set to 24 Mb.
```

GFlags 可以更改用户模式堆栈跟踪数据库的大小，但不会显示它。 若要显示跟踪数据库大小，请使用注册表 Api、 Regedit 中或注册表 (reg.exe)，Windows XP 和 Windows Server 2003 中包含的工具检查的值**StackTraceDatabaseSizeInMB**注册表项 (HKLM\\软件\\Microsoft\\Windows NT\\CurrentVersion\\图像 File Execution Options\\*映像文件名*\\ **StackTraceDatabaseSizeInMB**)。

(Reg 版本包含在 Windows XP 中，但该版本不允许 **/v**并 **/s**交换机在同一命令中的。)

下面的命令使用注册表来查询的值**StackTraceDatabaseSizeInMB**:

```console
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\MyApp.exe" /v StackTraceDatabaseSizeInMB 
```

在响应中，注册表中显示的值**StackTraceDatabaseSizeInMB**，这可确认的新值，24 (从 0x18) 设置。 重新启动 myapp.exe 时，此值才会生效。

```console
! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\MyApp.exe
    StackTraceDatabaseSizeInMB  REG_DWORD       0x18
```

**提示**  类型**reg 查询**命令到记事本中，然后将文件另存 tracedb.bat。 此后，若要显示的值**StackTraceDatabaseSizeInMB**，只需键入**TraceDb**。

 

 

 





