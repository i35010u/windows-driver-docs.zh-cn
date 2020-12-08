---
title: 示例8放大 User-Mode 堆栈跟踪数据库
description: 示例8放大 User-Mode 堆栈跟踪数据库
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 53fa8287de3fa3c21f65aff98e88a0ca953ac2fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838225"
---
# <a name="example-8-enlarging-the-user-mode-stack-trace-database"></a>示例8：放大 User-Mode 堆栈跟踪数据库


## <span id="ddk_example_8___enlarging_the_user_mode_stack_trace_database_dtools"></span><span id="DDK_EXAMPLE_8___ENLARGING_THE_USER_MODE_STACK_TRACE_DATABASE_DTOOLS"></span>


下面的 GFlags 命令会将 myapp.exe 的用户模式堆栈跟踪数据库的最大大小从 8 MB 增加到 24 MB。

该命令使用 **/i** 参数指定映像文件。 它使用 **/tracedb** 参数来设置最大堆栈跟踪数据库大小，并使用值24来指示大小（以 mb 为单位）。 该命令使用小数单位。  (的十六进制单位无效。 ) 

```console
gflags /i MyApp.exe /tracedb 24
```

如以下错误消息所示，此命令将失败，因为没有为 MyApp 映像文件设置 [创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md) (+ ust) 标志。 只有在创建跟踪数据库之后，才能设置跟踪数据库的大小。

```console
Failed to set the trace database size for `MyApp.exe'
```

以下命令将修复错误。 第一个命令为 myapp.exe 创建跟踪数据库，第二个命令将跟踪数据库的最大大小设置为 24 MB。 不能将这些命令合并到单个命令中。 下面的显示显示来自 GFlags 的命令和成功消息。

```console
gflags /i MyApp.exe +ust

Current Registry Settings for MyApp.exe executable are: 00001000
    ust - Create user mode stack trace database

gflags /i MyApp.exe /tracedb 24

Trace database size for `MyApp.exe' set to 24 Mb.
```

GFlags 可以更改用户模式堆栈跟踪数据库的大小，但不会显示。 若要显示跟踪数据库大小，请使用注册表 api、Regedit 或 Reg ( # A0) ，它是 Windows XP 和 windows Server 2003 中包含的一种工具，用于检查 **StackTraceDatabaseSizeInMB** 注册表项的值 (HKLM \\ Software \\ Microsoft \\ Windows NT \\ CurrentVersion \\ Image File 执行 Options \\ *ImageFileName* \\ **StackTraceDatabaseSizeInMB**) 。

Windows XP 中包含了 (Reg 版本，但该版本不允许在同一命令中使用 **/v** 和 **/s** 开关。 ) 

以下命令使用 Reg 查询 **StackTraceDatabaseSizeInMB** 的值：

```console
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\MyApp.exe" /v StackTraceDatabaseSizeInMB 
```

在响应中，Reg 显示 **StackTraceDatabaseSizeInMB** 的值，它确定已设置新值 24 (0x18) 。 重新启动 myapp.exe 时，此值会生效。

```console
! REG.EXE VERSION 3.0

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\MyApp.exe
    StackTraceDatabaseSizeInMB  REG_DWORD       0x18
```

**提示**   在记事本中键入 **reg query** 命令，然后将该文件保存为 tracedb.bat。 此后，若要显示 **StackTraceDatabaseSizeInMB** 的值，只需键入 **TraceDb**。

 

 

 





