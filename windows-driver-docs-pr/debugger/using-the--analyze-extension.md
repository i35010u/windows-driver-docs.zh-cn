---
title: 使用分析扩展
description: 使用分析扩展
ms.assetid: 0aa74153-e992-4d1c-b734-ccc60cff452c
keywords:
- 分析扩展，示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24547e89ed4a3a7c09fb8c43e0645fddd34dac6c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378473"
---
# <a name="using-the-analyze-extension"></a>使用 !analyze 扩展


## <span id="ddk_using_the_analyze_extension_dbg"></span><span id="DDK_USING_THE_ANALYZE_EXTENSION_DBG"></span>


调试崩溃的目标计算机或应用程序的第一步是使用[ **！ 分析**](-analyze.md)扩展命令。

此扩展不执行自动分析在很大程度。 在调试器命令窗口中显示此分析的结果。

应使用 **-v**完全详细显示数据的选项。 有关其他选项的详细信息，请参阅[ **！ 分析**](-analyze.md)参考页。

本主题包含：

- 用户模式 ！ 分析-v 示例
- 内核模式 ！ 分析-v 示例
- 跟进字段和 triage.ini 文件
- 其他 ！ 分析技术

### <a name="span-idddkausermodeanalyzevexampledbgspanspan-idddkausermodeanalyzevexampledbgspana-user-mode-analyze--v-example"></a><span id="ddk_a_user_mode_analyze_v_example_dbg"></span><span id="DDK_A_USER_MODE_ANALYZE_V_EXAMPLE_DBG"></span>用户模式 ！ 分析-v 示例

在此示例中，调试器附加到的用户模式应用程序遇到了异常。

```dbgcmd
0:000> !analyze -v
*******************************************************************************
*                                                                             *
*                        Exception Analysis                                   *
*                                                                             *
*******************************************************************************

Debugger SolutionDb Connection::Open failed 80004005
```

如果连接到 internet 时，调试器会尝试访问的崩溃解决方案由 Microsoft 维护的数据库。 在这种情况下，显示一条错误消息，指示你的计算机无法访问 internet 或不使用 web 站点。

```dbgcmd
FAULTING_IP: 
ntdll!PropertyLengthAsVariant+73
77f97704 cc               int     3
```

故障\_IP 字段中显示错误的时间的指令指针。

```dbgcmd
EXCEPTION_RECORD:  ffffffff -- (.exr ffffffffffffffff)
ExceptionAddress: 77f97704 (ntdll!PropertyLengthAsVariant+0x00000073)
   ExceptionCode: 80000003 (Break instruction exception)
  ExceptionFlags: 00000000
NumberParameters: 3
   Parameter[0]: 00000000
   Parameter[1]: 00010101
   Parameter[2]: ffffffff
```

异常\_记录字段显示了此故障的异常记录。 此外可以通过查看此信息[ **.exr （显示异常记录）** ](-exr--display-exception-record-.md)命令。

```dbgcmd
BUGCHECK_STR:  80000003
```

检测的错误\_STR 字段显示的异常代码。 该名称是用词不当，术语*bug 检查*实际上表示内核模式崩溃。 在用户模式调试中，将显示异常代码 — 在本例中为 0x80000003。

```dbgcmd
DEFAULT_BUCKET_ID:  APPLICATION_FAULT
```

默认值\_存储桶\_ID 字段显示属于此故障的故障的一般类别。

```dbgcmd
PROCESS_NAME:  MyApp.exe
```

该过程\_名称字段指定的进程引发异常的名称。

```dbgcmd
LAST_CONTROL_TRANSFER:  from 01050963 to 77f97704
```

上次\_控制\_传输字段显示的最后一个调用堆栈上。 在这种情况下，在地址 0x01050963 代码在 0x77F97704 调用一个函数。 可以使用这些地址与[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令，以确定这些地址位于哪些模块和函数。

```dbgcmd
STACK_TEXT:  
0006b9dc 01050963 00000000 0006ba04 000603fd ntdll!PropertyLengthAsVariant+0x73
0006b9f0 010509af 00000002 0006ba04 77e1a449 MyApp!FatalErrorBox+0x55 [D:\source_files\MyApp\util.c @ 541]
0006da04 01029f4e 01069850 0000034f 01069828 MyApp!ShowAssert+0x47 [D:\source_files\MyApp\util.c @ 579]
0006db6c 010590c3 000e01ea 0006fee4 0006feec MyApp!SelectColor+0x103 [D:\source_files\MyApp\colors.c @ 849]
0006fe04 77e11d0a 000e01ea 00000111 0000413c MyApp!MainWndProc+0x1322 [D:\source_files\MyApp\MyApp.c @ 1031]
0006fe24 77e11bc8 01057da1 000e01ea 00000111 USER32!UserCallWinProc+0x18
0006feb0 77e172b4 0006fee4 00000001 010518bf USER32!DispatchMessageWorker+0x2d0
0006febc 010518bf 0006fee4 00000000 01057c5d USER32!DispatchMessageA+0xb
0006fec8 01057c5d 0006fee4 77f82b95 77f83920 MyApp!ProcessQCQPMessage+0x3b [D:\source_files\MyApp\util.c @ 2212]
0006ff70 01062cbf 00000001 00683ed8 00682b88 MyApp!main+0x1e6 [D:\source_files\MyApp\MyApp.c @ 263]
0006ffc0 77e9ca90 77f82b95 77f83920 7ffdf000 MyApp!mainCRTStartup+0xff [D:\source_files\MyApp\crtexe.c @ 338]
0006fff0 00000000 01062bc0 00000000 000000c8 KERNEL32!BaseProcessStart+0x3d
```

堆栈\_文本字段显示出错的组件的堆栈跟踪。

```dbgcmd
FOLLOWUP_IP: 
MyApp!FatalErrorBox+55
01050963 5e               pop     esi

FOLLOWUP_NAME:  dbg

SYMBOL_NAME:  MyApp!FatalErrorBox+55

MODULE_NAME:  MyApp

IMAGE_NAME:  MyApp.exe

DEBUG_FLR_IMAGE_TIMESTAMP:  383490a9
```

当[ **！ 分析**](-analyze.md)确定可能导致错误，说明其显示在后续\_IP 字段。 符号\_名称、 模块\_名称、 映像\_名称和调试\_FLR\_图像\_时间戳字段显示符号、 模块、 映像名称和与此相对应的映像时间戳指令。

```dbgcmd
STACK_COMMAND:  .ecxr ; kb
```

堆栈\_命令字段显示的命令，用于获取堆栈\_文本。 可以使用此命令来重复此堆栈跟踪显示，或更改它以获取相关的堆栈信息。

```dbgcmd
BUCKET_ID:  80000003_MyApp!FatalErrorBox+55
```

存储桶\_ID 字段显示特定类别的当前失败所属的故障。 此类别可帮助确定要在分析输出中显示的其他信息的调试器。

```dbgcmd
Followup: dbg
---------
```

有关后续信息\_名称和后续字段，请参阅后续字段和 triage.ini 文件。

有多种可能会出现其他字段：

-   如果控件已转让给无效的地址，然后故障\_IP 字段将包含此无效地址。 而不是继续努力\_IP 字段中，失败\_指令\_地址字段将显示此地址中的反汇编的代码，尽管此反汇编可能是没有意义。 在此情况下，该符号\_名称、 模块\_名称、 映像\_名称和调试\_FLR\_图像\_时间戳字段将指向此指令的调用方。

-   如果处理器 misfires，可能会看到单个\_位\_错误，两个\_位\_错误或可能\_无效\_控制\_传输字段。

-   如果内存损坏似乎发生了，CHKIMG\_将指定扩展字段[ **！ chkimg** ](-chkimg.md)应该用于调查的扩展命令。

### <a name="span-idddkakernelmodeanalyzevexampledbgspanspan-idddkakernelmodeanalyzevexampledbgspana-kernel-mode-analyze--v-example"></a><span id="ddk_a_kernel_mode_analyze_v_example_dbg"></span><span id="DDK_A_KERNEL_MODE_ANALYZE_V_EXAMPLE_DBG"></span>内核模式 ！ 分析-v 示例

在此示例中，调试器附加到已只是崩溃的计算机。

```dbgcmd
kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DRIVER_IRQL_NOT_LESS_OR_EQUAL (d1)
An attempt was made to access a pagable (or completely invalid) address at an
interrupt request level (IRQL) that is too high.  This is usually
caused by drivers using improper addresses.
If kernel debugger is available get stack backtrace.
```

显示的第一个元素显示 bug 检查代码和有关 bug 检查此类型的信息。 某些显示的文本可能不适用于此特定实例。 每个 bug 检查的更多详细信息，请参阅[Bug 检查代码参考](bug-check-code-reference2.md)部分。

```dbgcmd
Arguments:
Arg1: 00000004, memory referenced
Arg2: 00000002, IRQL
Arg3: 00000001, value 0 = read operation, 1 = write operation
Arg4: f832035c, address which referenced memory
```

接下来显示 bug 检查参数。 它们是每个后跟说明。 例如，第三个参数为 1，且其后的注释解释了，这指示写操作失败。

```dbgcmd
## Debugging Details:


WRITE_ADDRESS:  00000004 Nonpaged pool

CURRENT_IRQL:  2
```

下一步的几个字段在发生崩溃的性质而异。 在这种情况下，我们看到写入\_地址和当前\_IRQL 字段。 这些只需将复述 bug 检查参数中所示的信息。 通过比较语句"非分页的池"为"已尝试访问 pagable （或完全无效） 地址"中读取的 bug 检查文本，我们可以看到的地址无效。 无效的地址在这种情况下为 0x00000004。

```dbgcmd
FAULTING_IP: 
USBPORT!USBPORT_BadRequestFlush+7c
f832035c 894204           mov     [edx+0x4],eax
```

故障\_IP 字段中显示错误的时间的指令指针。

```dbgcmd
DEFAULT_BUCKET_ID:  DRIVER_FAULT
```

默认值\_存储桶\_ID 字段显示属于此故障的故障的一般类别。

```dbgcmd
BUGCHECK_STR:  0xD1
```

检测的错误\_STR 字段显示的 bug 检查代码，我们已经看到了。 在某些情况下附加的会审信息都会追加。

```dbgcmd
TRAP_FRAME:  f8950dfc -- (.trap fffffffff8950dfc)
.trap fffffffff8950dfc
ErrCode = 00000002
eax=81cc86dc ebx=81cc80e0 ecx=81e55688 edx=00000000 esi=81cc8028 edi=8052cf3c
eip=f832035c esp=f8950e70 ebp=f8950e90 iopl=0         nv up ei pl nz ac po nc
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00010216
USBPORT!USBPORT_BadRequestFlush+7c:
f832035c 894204           mov     [edx+0x4],eax     ds:0023:00000004=????????
.trap
Resetting default context
```

陷阱\_帧字段显示了此故障的陷阱帧。 此外可以通过查看此信息[ **.trap （显示陷阱帧）** ](-trap--display-trap-frame-.md)命令。

```dbgcmd
LAST_CONTROL_TRANSFER:  from f83206e0 to f832035c
```

上次\_控制\_传输字段显示的最后一个调用堆栈上。 在这种情况下，在地址 0xF83206E0 代码在 0xF832035C 调用一个函数。 可以使用[ **ln （列表最接近符号）** ](ln--list-nearest-symbols-.md)命令，以确定这些地址位于哪些模块和函数。

```dbgcmd
STACK_TEXT:  
f8950e90 f83206e0 024c7262 00000000 f8950edc USBPORT!USBPORT_BadRequestFlush+0x7c
f8950eb0 804f5561 81cc8644 81cc8028 6d9a2f30 USBPORT!USBPORT_DM_TimerDpc+0x10c
f8950fb4 804f5644 6e4be98e 00000000 ffdff000 nt!KiTimerListExpire+0xf3
f8950fe0 8052c47c 8053cf20 00000000 00002e42 nt!KiTimerExpiration+0xb0
f8950ff4 8052c16a efdefd44 00000000 00000000 nt!KiRetireDpcList+0x31
```

堆栈\_文本字段显示出错的组件的堆栈跟踪。

```dbgcmd
FOLLOWUP_IP: 
USBPORT!USBPORT_BadRequestFlush+7c
f832035c 894204           mov     [edx+0x4],eax
```

跟进\_IP 字段显示可能导致错误的指令的反汇编。

```dbgcmd
FOLLOWUP_NAME:  usbtri

SYMBOL_NAME:  USBPORT!USBPORT_BadRequestFlush+7c

MODULE_NAME:  USBPORT

IMAGE_NAME:  USBPORT.SYS

DEBUG_FLR_IMAGE_TIMESTAMP:  3b7d868b
```

符号\_名称、 模块\_名称、 映像\_名称和 DBG\_FLR\_图像\_时间戳字段显示符号、 模块、 图像和对应于此指令的映像时间戳（如果它是有效的），或向此指令 （如果不存在） 的调用方。

```dbgcmd
STACK_COMMAND:  .trap fffffffff8950dfc ; kb
```

堆栈\_命令字段显示的命令，用于获取堆栈\_文本。 可以使用此命令来重复此堆栈跟踪显示，或更改它以获取相关的堆栈信息。

```dbgcmd
BUCKET_ID:  0xD1_W_USBPORT!USBPORT_BadRequestFlush+7c
```

存储桶\_ID 字段显示特定类别的当前失败所属的故障。 此类别可帮助确定要在分析输出中显示的其他信息的调试器。

```dbgcmd
INTERNAL_SOLUTION_TEXT:  https://oca.microsoft.com/resredir.asp?sid=62&State=1
```

如果连接到 internet 时，调试器会尝试访问的崩溃解决方案由 Microsoft 维护的数据库。 此数据库包含大量具有已知错误有关的信息的网页的链接。 如果你遇到的问题，内部找到匹配项\_解决方案\_文本字段将显示一个 URL，您可以访问有关详细信息。

```dbgcmd
Followup: usbtri
---------

      This problem has a known fix.
      Please connect to the following URL for details:
      ------------------------------------------------
      https://oca.microsoft.com/resredir.asp?sid=62&State=1
```

有关后续信息\_名称和后续字段，请参阅后续字段和 triage.ini 文件：

有多种可能会出现其他字段：

-   如果控件已转让给无效的地址，然后故障\_IP 字段将包含此无效地址。 而不是继续努力\_IP 字段中，失败\_指令\_地址字段将显示此地址中的反汇编的代码，尽管此反汇编可能是没有意义。 在此情况下，该符号\_名称、 模块\_名称、 映像\_名称和 DBG\_FLR\_图像\_时间戳字段将指向此指令的调用方。

-   如果处理器 misfires，可能会看到单个\_位\_错误，两个\_位\_错误或可能\_无效\_控制\_传输字段。

-   如果内存损坏似乎发生了，CHKIMG\_将指定扩展字段[ **！ chkimg** ](-chkimg.md)应该用于调查的扩展命令。

-   如果设备驱动程序的代码中出现的 bug 检查，其名称可能显示在 BUGCHECKING\_驱动程序字段。

### <a name="span-idddkthefollowupfieldandthetriageinifiledbgspanspan-idddkthefollowupfieldandthetriageinifiledbgspanthe-followup-field-and-the-triageini-file"></a><span id="ddk_the_followup_field_and_the_triage_ini_file_dbg"></span><span id="DDK_THE_FOLLOWUP_FIELD_AND_THE_TRIAGE_INI_FILE_DBG"></span>跟进字段和 triage.ini 文件

在用户模式和内核模式中，在显示中的后续字段将显示所有者信息的当前堆栈帧，如果可确定此信息。 此信息按以下方式确定：

1.  当[ **！ 分析**](-analyze.md)扩展，则调试器开始在堆栈中的顶帧，并确定是否为导致错误。 如果不是这样，则会分析下一帧。 此过程将继续，直到找到可能有故障的帧。

2.  调试器会尝试确定模块和在此范围内的函数的所有者。 如果可以确定所有者，此帧将被视为可出错。

3.  如果无法确定所有者，调试器将传递到下一步的堆栈帧和等等中,，直到确定所有者 （或完全检查堆栈）。 在此搜索中找到其所有者的第一帧被视为错误。 如果堆栈不包含找到的任何信息已用尽，则会不显示任何后续字段。

4.  跟进字段中显示错误的帧的所有者。 如果 **！ 分析-v**是使用跟进\_IP、 符号\_名称、 模块\_名称、 映像\_名称和 DBG\_FLR\_映像\_时间戳字段将引用到此帧。

对于要显示的有用信息的后续字段，必须首先创建包含所有者名称的模块和函数的 Triage.ini 文件。

Triage.ini 文件应确定可能具有错误的所有模块的所有者。 可以使用一个信息性的字符串而不是实际的所有者，但此字符串不能包含空格。 如果确定模块不会发生错误，可以省略此模块或指示它应被跳过。 还有可能指定各个函数的所有者为会审过程提供更精细的粒度。

Triage.ini 文件的语法的详细信息，请参阅[指定的模块和函数所有者](specifying-module-and-function-owners.md)。

### <a name="span-idddkadditionalanalyzetechniquesdbgspanspan-idddkadditionalanalyzetechniquesdbgspanadditional-analyze-techniques"></a><span id="ddk_additional_analyze_techniques_dbg"></span><span id="DDK_ADDITIONAL_ANALYZE_TECHNIQUES_DBG"></span>其他 ！ 分析技术

如果您不相信，存储桶\_ID 是正确的可以通过使用的存储桶选择重写[ **！ 分析**](-analyze.md)与 **-D**参数。

如果不发生任何崩溃或异常情况， [ **！ 分析**](-analyze.md)将显示为提供目标的当前状态很短的文本。 在某些情况下您可能想要强制分析才能开始，如果出现崩溃。 使用 **！ 分析-f**来完成此任务。

在用户模式下，如果发生了异常，但您认为根本问题是一个挂起的线程，将当前线程设置为你正在调查，然后使用的线程 **！ 分析-挂起**。 此扩展将执行线程堆栈分析，以确定任何线程正在阻止其他线程。

在内核模式下，如果发生错误检查，但您认为基础问题是挂起的线程，请使用 **！ 分析-挂起**。 此扩展将调查系统持有的锁和扫描的 DPC 队列链，并且会显示挂起线程的迹象。 如果您认为该问题是内核模式资源死锁，请使用[ **！ 死锁**](-deadlock.md)扩展插件和**死锁检测**Driver Verifier 选项。

此外会自动可以忽略已知的问题。 若要执行此操作，必须首先创建包含带格式的已知问题列表的 XML 文件。 使用 * *！ 分析-c-加载 * * * KnownIssuesFile*扩展来加载此文件。 当发生异常或中断，然后使用 **！ 分析-c**扩展。 如果异常与匹配的其中一个已知问题，目标将继续执行。 如果目标不会继续执行，则可以使用 **！ 分析-v**以确定问题的原因。 示例 XML 文件可以在 sdk 中找到\\示例\\分析\_继续调试程序安装目录的子目录。

 

 





