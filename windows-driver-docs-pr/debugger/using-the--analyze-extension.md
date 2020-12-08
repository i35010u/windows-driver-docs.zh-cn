---
title: 使用分析扩展
description: 使用分析扩展
keywords:
- 分析扩展，示例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8257a94310fd83a04e106e4aa7eace5ab25a7ca5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803055"
---
# <a name="using-the-analyze-extension"></a>使用 !analyze 扩展


## <span id="ddk_using_the_analyze_extension_dbg"></span><span id="DDK_USING_THE_ANALYZE_EXTENSION_DBG"></span>


调试损坏的目标计算机或应用程序的第一步是使用 [**！分析**](-analyze.md) 扩展命令。

此扩展会执行大量的自动分析。 此分析的结果将显示在调试器命令窗口中。

应使用 **-v** 选项来完全详细地显示数据。 有关其他选项的详细信息，请参阅 [**！分析**](-analyze.md) 引用页。

本主题包含：

- User-Mode！分析-v 示例
- Kernel-Mode！分析-v 示例
- 跟进字段和 triage.ini 文件
- 其他！分析技术

### <a name="span-idddk_a_user_mode_analyze_v_example_dbgspanspan-idddk_a_user_mode_analyze_v_example_dbgspana-user-mode-analyze--v-example"></a><span id="ddk_a_user_mode_analyze_v_example_dbg"></span><span id="DDK_A_USER_MODE_ANALYZE_V_EXAMPLE_DBG"></span>User-Mode！分析-v 示例

在此示例中，将调试器附加到遇到异常的用户模式应用程序。

```dbgcmd
0:000> !analyze -v
*******************************************************************************
*                                                                             *
*                        Exception Analysis                                   *
*                                                                             *
*******************************************************************************

Debugger SolutionDb Connection::Open failed 80004005
```

如果已连接到 internet，则调试器将尝试访问由 Microsoft 维护的故障解决方案数据库。 在这种情况下，会显示一条错误消息，指示您的计算机无法访问 internet 或网站未运行。

```dbgcmd
FAULTING_IP: 
ntdll!PropertyLengthAsVariant+73
77f97704 cc               int     3
```

\_错误 IP 字段显示错误时的指令指针。

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

"异常 \_ 记录" 字段显示此崩溃的异常记录。 还可以使用 [**. .exr (显示异常记录)**](-exr--display-exception-record-.md) 命令来查看此信息。

```dbgcmd
BUGCHECK_STR:  80000003
```

"错误检查 \_ 字符串" 字段显示异常代码。 名称是 misnomer，术语 " *bug 检查* " 实际上表示内核模式崩溃。 在用户模式调试中，将显示异常代码（在本例中为0x80000003）。

```dbgcmd
DEFAULT_BUCKET_ID:  APPLICATION_FAULT
```

"默认 \_ BUCKET \_ ID" 字段显示此失败所属的故障的一般类别。

```dbgcmd
PROCESS_NAME:  MyApp.exe
```

"进程 \_ 名称" 字段指定引发异常的进程的名称。

```dbgcmd
LAST_CONTROL_TRANSFER:  from 01050963 to 77f97704
```

最后一个 \_ 控件 \_ 传输字段显示堆栈上的最后一次调用。 在这种情况下，位于地址0x01050963 的代码在0x77F97704 调用了函数。 可以将这些地址与 [**ln (列出最接近符号)**](ln--list-nearest-symbols-.md) 命令一起使用，以确定这些地址驻留的模块和函数。

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

"堆栈 \_ 文本" 字段显示出错组件的堆栈跟踪。

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

当 [**！分析**](-analyze.md) 确定可能导致错误的指令时，它将在 "后续 IP" 字段中显示 \_ 。 符号 \_ 名称、模块 \_ 名称、映像 \_ 名称和 DEBUG \_ FLR \_ 映像 \_ 时间戳字段显示与此指令相对应的符号、模块、图像名称和图像时间戳。

```dbgcmd
STACK_COMMAND:  .ecxr ; kb
```

"堆栈 \_ 命令" 字段显示用于获取堆栈文本的命令 \_ 。 可以使用此命令重复此堆栈跟踪显示，或将其更改为获取相关的堆栈信息。

```dbgcmd
BUCKET_ID:  80000003_MyApp!FatalErrorBox+55
```

BUCKET \_ ID 字段显示当前故障所属的特定失败类别。 此类别有助于调试器确定要在分析输出中显示的其他信息。

```dbgcmd
Followup: dbg
---------
```

有关跟进 \_ 名称和后续字段的信息，请参阅跟进字段和 triage.ini 文件。

可能会出现许多其他字段：

-   如果控件被传输到无效地址，则出错的 \_ IP 字段将包含此无效地址。 \_ \_ \_ 尽管此反汇编可能毫无意义，但 "失败的指令地址" 字段不会显示此地址中的反汇编代码。 在这种情况下，符号 \_ 名称、模块 \_ 名称、映像 \_ 名称和 DEBUG \_ FLR \_ 映像 \_ 时间戳字段将引用此指令的调用方。

-   如果处理器 misfires，则可能会出现单一 \_ 位 \_ 错误、两 \_ 位 \_ 错误或可能的 \_ 无效 \_ 控件 \_ 传输字段。

-   如果似乎发生了内存损坏，CHKIMG \_ 扩展字段将指定应该用于调查的 [**！ CHKIMG**](-chkimg.md) 扩展命令。

### <a name="span-idddk_a_kernel_mode_analyze_v_example_dbgspanspan-idddk_a_kernel_mode_analyze_v_example_dbgspana-kernel-mode-analyze--v-example"></a><span id="ddk_a_kernel_mode_analyze_v_example_dbg"></span><span id="DDK_A_KERNEL_MODE_ANALYZE_V_EXAMPLE_DBG"></span>Kernel-Mode！分析-v 示例

在此示例中，将调试器附加到刚刚崩溃的计算机。

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

显示的第一个元素显示 bug 检查代码以及有关此类型 bug 检查的信息。 某些显示的文本可能不适用于此特定实例。 有关每个 bug 检查的详细信息，请参阅 [Bug 检查代码参考](bug-check-code-reference2.md) 部分。

```dbgcmd
Arguments:
Arg1: 00000004, memory referenced
Arg2: 00000002, IRQL
Arg3: 00000001, value 0 = read operation, 1 = write operation
Arg4: f832035c, address which referenced memory
```

随后将显示 bug 检查参数。 它们分别后跟说明。 例如，第三个参数为1，后面的注释说明这表明写操作失败。

```dbgcmd
## Debugging Details:


WRITE_ADDRESS:  00000004 Nonpaged pool

CURRENT_IRQL:  2
```

接下来的几个字段根据崩溃的性质而有所不同。 在这种情况下，我们将看到 "写入 \_ 地址" 和 "当前 \_ IRQL" 字段。 它们只是重述错误检查参数中显示的信息。 通过将语句 "非分页池" 与 bug 检查文本进行比较，该文本会显示 "尝试访问 pagable (或完全无效的) 地址"），我们可以看到该地址是无效的。 在此情况下，无效地址为0x00000004。

```dbgcmd
FAULTING_IP: 
USBPORT!USBPORT_BadRequestFlush+7c
f832035c 894204           mov     [edx+0x4],eax
```

\_错误 IP 字段显示错误时的指令指针。

```dbgcmd
DEFAULT_BUCKET_ID:  DRIVER_FAULT
```

"默认 \_ BUCKET \_ ID" 字段显示此失败所属的故障的一般类别。

```dbgcmd
BUGCHECK_STR:  0xD1
```

"错误检测 \_ 字符串" 字段显示已查看的 bug 检查代码。 在某些情况下，附加的会审信息将追加。

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

"陷阱 \_ 帧" 字段显示此崩溃的捕获帧。 此信息还可以通过使用 [**(显示陷印帧)**](-trap--display-trap-frame-.md) 命令查看。

```dbgcmd
LAST_CONTROL_TRANSFER:  from f83206e0 to f832035c
```

最后一个 \_ 控件 \_ 传输字段显示堆栈上的最后一次调用。 在这种情况下，位于地址0xF83206E0 的代码在0xF832035C 调用了函数。 您可以使用 [**ln (列出最接近符号)**](ln--list-nearest-symbols-.md) 命令来确定这些地址驻留在哪个模块和函数中。

```dbgcmd
STACK_TEXT:  
f8950e90 f83206e0 024c7262 00000000 f8950edc USBPORT!USBPORT_BadRequestFlush+0x7c
f8950eb0 804f5561 81cc8644 81cc8028 6d9a2f30 USBPORT!USBPORT_DM_TimerDpc+0x10c
f8950fb4 804f5644 6e4be98e 00000000 ffdff000 nt!KiTimerListExpire+0xf3
f8950fe0 8052c47c 8053cf20 00000000 00002e42 nt!KiTimerExpiration+0xb0
f8950ff4 8052c16a efdefd44 00000000 00000000 nt!KiRetireDpcList+0x31
```

"堆栈 \_ 文本" 字段显示出错组件的堆栈跟踪。

```dbgcmd
FOLLOWUP_IP: 
USBPORT!USBPORT_BadRequestFlush+7c
f832035c 894204           mov     [edx+0x4],eax
```

"后续 \_ IP" 字段显示可能导致错误的指令的反汇编。

```dbgcmd
FOLLOWUP_NAME:  usbtri

SYMBOL_NAME:  USBPORT!USBPORT_BadRequestFlush+7c

MODULE_NAME:  USBPORT

IMAGE_NAME:  USBPORT.SYS

DEBUG_FLR_IMAGE_TIMESTAMP:  3b7d868b
```

符号 \_ 名称、模块 \_ 名称、映像 \_ 名称和 DBG \_ FLR \_ 映像 \_ 时间戳字段显示与此指令相对应的符号、模块、图像和图像时间戳 (如果它是有效) ，则为; 如果未) ，则为此指令 (的调用方。

```dbgcmd
STACK_COMMAND:  .trap fffffffff8950dfc ; kb
```

"堆栈 \_ 命令" 字段显示用于获取堆栈文本的命令 \_ 。 可以使用此命令重复此堆栈跟踪显示，或将其更改为获取相关的堆栈信息。

```dbgcmd
BUCKET_ID:  0xD1_W_USBPORT!USBPORT_BadRequestFlush+7c
```

BUCKET \_ ID 字段显示当前故障所属的特定失败类别。 此类别有助于调试器确定要在分析输出中显示的其他信息。

```dbgcmd
INTERNAL_SOLUTION_TEXT:  https://oca.microsoft.com/resredir.asp?sid=62&State=1
```

如果已连接到 internet，则调试器将尝试访问由 Microsoft 维护的故障解决方案数据库。 此数据库包含大量包含已知 bug 相关信息的网页的链接。 如果找到了与您的问题相符的匹配项，则 "内部 \_ 解决方案 \_ 文本" 字段将显示一个 URL，您可以访问该 URL 以获取详细信息。

```dbgcmd
Followup: usbtri
---------

      This problem has a known fix.
      Please connect to the following URL for details:
      ------------------------------------------------
      https://oca.microsoft.com/resredir.asp?sid=62&State=1
```

有关跟进 \_ 名称和后续字段的信息，请参阅跟进字段和 triage.ini 文件：

可能会出现许多其他字段：

-   如果控件被传输到无效地址，则出错的 \_ IP 字段将包含此无效地址。 \_ \_ \_ 尽管此反汇编可能毫无意义，但 "失败的指令地址" 字段不会显示此地址中的反汇编代码。 在这种情况下，符号 \_ 名称、模块 \_ 名称、映像 \_ 名称和 DBG \_ FLR \_ 映像 \_ 时间戳字段将引用此指令的调用方。

-   如果处理器 misfires，则可能会出现单一 \_ 位 \_ 错误、两 \_ 位 \_ 错误或可能的 \_ 无效 \_ 控件 \_ 传输字段。

-   如果似乎发生了内存损坏，CHKIMG \_ 扩展字段将指定应该用于调查的 [**！ CHKIMG**](-chkimg.md) 扩展命令。

-   如果在设备驱动程序的代码中发生了错误检查，则其名称可能会显示在 BUGCHECKING \_ 驱动程序字段中。

### <a name="span-idddk_the_followup_field_and_the_triage_ini_file_dbgspanspan-idddk_the_followup_field_and_the_triage_ini_file_dbgspanthe-followup-field-and-the-triageini-file"></a><span id="ddk_the_followup_field_and_the_triage_ini_file_dbg"></span><span id="DDK_THE_FOLLOWUP_FIELD_AND_THE_TRIAGE_INI_FILE_DBG"></span>跟进字段和 triage.ini 文件

在用户模式和内核模式下，显示中的 "跟进" 字段将显示有关当前堆栈帧的所有者的信息（如果可以确定）。 此信息按以下方式确定：

1.  使用 [**！分析**](-analyze.md) 扩展时，调试器将从堆栈中的顶部帧开始，并确定它是否负责错误。 如果不是，则分析下一帧。 此过程将继续，直到找到可能处于错误状态的帧。

2.  调试器将尝试确定此帧中的模块和函数的所有者。 如果可以确定所有者，则将此帧视为错误。

3.  如果无法确定所有者，则调试器会传递到下一个堆栈帧，依此类推，直到确定所有者 (或) 完全检查堆栈。 在此搜索中找到其所有者的第一个帧被视为错误。 如果未找到任何信息就用尽了堆栈，则不会显示任何跟进字段。

4.  出现错误的帧所有者显示在 "开始" 字段中。 如果使用了 **！分析-v** ，则后续 \_ IP、符号 \_ 名称、模块 \_ 名称、映像 \_ 名称和 DBG \_ FLR \_ 映像 \_ 时间戳字段将引用此帧。

要使 "后续" 字段显示有用信息，必须首先创建一个 Triage.ini 文件，该文件包含 module 和 function 物主的名称。

Triage.ini 文件应该确定可能有错误的所有模块的所有者。 您可以使用信息字符串而不是实际所有者，但此字符串不能包含空格。 如果您确信某个模块不会出错，则可以省略此模块或指示应跳过它。 还可以指定各个函数的所有者，为会审过程提供更精细的粒度。

有关 Triage.ini 文件的语法的详细信息，请参阅 [指定 Module 和 Function 物主](specifying-module-and-function-owners.md)。

### <a name="span-idddk_additional_analyze_techniques_dbgspanspan-idddk_additional_analyze_techniques_dbgspanadditional-analyze-techniques"></a><span id="ddk_additional_analyze_techniques_dbg"></span><span id="DDK_ADDITIONAL_ANALYZE_TECHNIQUES_DBG"></span>其他！分析技术

如果你不认为 BUCKET \_ ID 是正确的，则可以通过使用 **-D** 参数的 [**！分析**](-analyze.md)来替代 bucket 选项。

如果未发生崩溃或异常， [**！ "分析**](-analyze.md) " 将显示一个非常短的文本，该文本提供目标的当前状态。 在某些情况下，你可能想要强制进行分析，就好像发生了故障。 使用 **！分析-f** 来完成此任务。

在用户模式下，如果发生了异常，但你认为根本问题是挂起的线程，请将当前线程设置为正在调查的线程，然后使用 **！分析-挂起**。 此扩展将执行线程堆栈分析以确定是否有任何线程正在阻止其他线程。

在内核模式下，如果发生 bug 检查但你认为根本问题是挂起的线程，请使用 **！分析-挂起**。 此扩展将调查系统持有的锁并扫描 DPC 队列链，并显示挂起线程的任何指示。 如果您认为此问题是内核模式资源死锁，请使用 [**！死锁**](-deadlock.md) 扩展以及驱动程序验证程序的 **死锁检测** 选项。

你还可以自动忽略已知问题。 为此，必须首先创建一个包含格式化的已知问题列表的 XML 文件。 使用 **！**_KnownIssuesFile_ 扩展加载此文件。 然后，当发生异常或中断时，请使用 **！分析-c** 扩展。 如果异常与其中一个已知问题匹配，则目标将继续执行。 如果目标未继续执行，则可以使用 **！分析-v** 确定问题的原因。 示例 XML 文件可以在 sdk \\ 示例 \\ \_ "分析继续" 子目录中的调试器安装目录中找到。

 

 





