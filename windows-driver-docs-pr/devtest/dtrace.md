---
title: Windows 上的 DTrace
description: DTrace 是一个命令行工具工具，用于显示系统信息和事件。
ms.assetid: abf23d76-423d-4d1e-afde-83739015bbfe
keywords:
- DTrace WDK
- 软件跟踪 WDK，DTrace
- 显示跟踪消息
- 格式化跟踪消息 WDK DTrace
- 跟踪消息格式 WDK DTrace
- 软件跟踪 WDK，设置消息格式
- 跟踪 WDK，DTrace
- 跟踪消息格式化文件 WDK
ms.date: 11/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: c0a699112132e517f24bdb2284af31cb14b5245c
ms.sourcegitcommit: 9e5a99dc75dfee3caa9a242adc0ed22ae4df9f29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89043111"
---
# <a name="dtrace-on-windows"></a>Windows 上的 DTrace

DTrace ( # A0) 是一个命令行工具，用于显示系统信息和事件。 DTrace 是移植到 windows 的开源跟踪平台。 DTrace 最初是为 Solaris 操作系统而开发的。  它提供用户/核心函数的动态检测功能，这是使用 D 语言推理跟踪编写脚本的能力。 此外，DTrace 还具有 Windows OS 特定扩展，如 ETW 检测、ETW 事件生成、系统调用探测和实时转储捕获功能。  

> [!NOTE]
> 版本18980和 Windows Server 有问必答 Preview 版本18975后，Windows 内部版本支持 DTrace。

Windows Github 站点上的 DTrace 位于此处：

[https://github.com/microsoft/DTrace-on-Windows](https://github.com/microsoft/DTrace-on-Windows)

## <a name="open-dtrace-information"></a>打开 DTrace 信息
  
有关 DTrace 的详细信息，请参阅剑桥大学的 [OpenDTrace 规范1.0 版](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-924.pdf) 。

主 GitHub 站点位于上 [https://github.com/opendtrace/](https://github.com/opendtrace/) 。

提供一组有用的脚本 [https://github.com/opendtrace/toolkit](https://github.com/opendtrace/toolkit) 。

提供了许多 DTrace 书籍，如：

*DTrace： Oracle Solaris 中的动态跟踪，Mac OS X 和 FreeBSD* By Brendan Gregg 和 Jim Mauro

*Solaris 性能和工具： solaris 10 和 OpenSolaris* By Richard McDougall、Jim Mauro 和 Brendan Gregg 的 DTRACE 和 MDB 技术

## <a name="providing-feedback-on-windows-dtrace"></a>在 Windows DTrace 上提供反馈

使用反馈中心请求新功能，或使用 Windows DTrace 报告任何问题或错误。

1. 通过选择此链接从 Windows 电脑启动反馈中心 [https://windows-feedback:?contextid=1053](https://windows-feedback:?contextid=1053) 。
2. 选择 " *添加新反馈*"。
3. 提供问题的详细特定说明或建议。

## <a name="dtrace-windows-extensions"></a>DTrace Windows 扩展

下面是一些可在 Windows 上使用的提供程序及其检测到的内容。

- syscall – NTOS 系统调用

- fbt (函数边界跟踪) –内核函数入口和返回

- pid (进程 ID) –用户模式进程跟踪。 如内核模式 FBT，还允许检测任意函数偏移量。

- 针对 Windows) 的 etw (事件跟踪–允许为 ETW 定义探测器此提供程序有助于利用 DTrace 中现有的操作系统检测。

### <a name="syscall"></a>SYSCALL

SYSCALL 为每个系统调用提供一对探测：输入系统调用之前触发的入口探测，以及在系统调用完成后，但在控制转移回用户级别之前触发的 return 探测器。 对于所有 SYSCALL 探测，函数名称设置为已检测系统调用的名称，模块名称是该函数所在的模块。 可以通过在命令提示符处键入命令来找到 SYSCALL 提供程序提供的系统调用的名称 `dtrace.exe -l -P syscall` 。 请注意，探测名称为小写。 命令 `dtrace -ln syscall:::` 还将列出 syscall 提供程序中提供的所有探测及其参数。

```dtrace
C:\> dtrace -ln syscall:::
  ID   PROVIDER            MODULE                          FUNCTION NAME
    6    syscall                                 NtWaitHighEventPair entry
    7    syscall                                 NtWaitHighEventPair return
    8    syscall                       NtRegisterThreadTerminatePort entry
    9    syscall                       NtRegisterThreadTerminatePort return
...
```

请注意，这些示例中不显示所有屏幕输出。 "..."用于表示截断后的输出。

若要在输出中滚动，请通过管道执行 *更多* 命令，如下所示：

`dtrace -ln syscall:::|more`

添加 v 选项以显示有关可用 syscall 探测的详细信息。

```dtrace
C:\> dtrace -lvn syscall:::
...

  942    syscall                                    NtSaveMergedKeys entry

        Probe Description Attributes
                Identifier Names: Private
                Data Semantics:   Private
                Dependency Class: ISA

        Argument Attributes
                Identifier Names: Private
                Data Semantics:   Private
                Dependency Class: ISA

        Argument Types
                args[0]: HANDLE
                args[1]: HANDLE
                args[2]: HANDLE
...
```

### <a name="etw"></a>ETW

 DTrace 包括对现有的列入/tracelogged ETW 探测的支持。 可以在事件触发时同步检测、筛选和分析 ETW 事件。 此外，可以使用 DTrace 将各种事件/系统状态组合在一起，以提供合并的输出流，以帮助调试复杂的错误情况。  

命令 `dtrace -ln etw:::` 将列出 syscall 提供程序中提供的所有探测及其参数。

```dtrace
  C:\> dtrace -ln etw:::
  ID   PROVIDER            MODULE                          FUNCTION NAME
  944        etw 048dc470-37c1-52a8-565a-54cb27be37ec           0xff_0xffffffffffffffff generic_event
  945        etw aab97afe-deaf-5882-1e3b-d7210f059dc1           0xff_0xffffffffffffffff generic_event
  946        etw b0f40491-9ea6-5fd5-ccb1-0ec63be8b674           0xff_0xffffffffffffffff generic_event
  947        etw 4ee869fa-9954-4b90-9a62-308c74f99d32           0xff_0xffffffffffffffff generic_event
  ...
  ```

有关详细信息，请参阅 [DTRACE ETW](dtrace-etw.md)。

### <a name="function-boundary-tracing-fbt"></a>函数边界跟踪 (FBT) 

函数边界跟踪 (FBT) 提供程序提供与条目关联的探测器，并从 Windows 内核中的大多数函数返回。 函数是程序文本的基本单位。 与其他 DTrace 提供程序类似，FBT 在未显式启用时没有探测效果。 启用后，FBT 仅在探测的函数中产生探测效果。 在 x86 和 x64 平台上已经实现了 FBT。

对于每个指令集，都有少量函数不调用其他函数，并且由编译器高度优化 (称为叶函数) 无法通过 FBT 进行检测。 DTrace 中不存在对这些函数的探测。

命令 `dtrace -ln fbt:nt::` 将列出可用于 nt 模块的所有探测及其参数。 使用 "调试器 [lm (列出加载的模块") ](https://docs.microsoft.com/windows-hardware/drivers/debugger/lm--list-loaded-modules-) 命令列出所有可用模块。

```dtrace
C:\>dtrace -ln "fbt:nt::"
   ID   PROVIDER            MODULE                          FUNCTION NAME
 3336        fbt                nt                PiDqActionDataFree entry
 3337        fbt                nt                PiDqActionDataFree return
 3338        fbt                nt PiDqActionDataGetRequestedProperties entry
 3339        fbt                nt PiDqActionDataGetRequestedProperties return
 3340        fbt                nt _CmGetMatchingFilteredDeviceInterfaceList entry
...
```

> [!NOTE]
> 由于在 nt 中可以使用上千个调用，因此在运行记录数据的 DTrace 命令时，将函数名称留空是不是一个好办法。 避免可能影响性能的建议方法是至少指定函数名称的一部分，例如 `fbt:nt:*Timer*:entry` 。

### <a name="pid"></a>PID

使用 DTrace PID 提供程序，可以跟踪用户模式进程（如 web 浏览器或数据库）的内部执行。 你还可以在启动进程时附加 DTrace，以便调试进程启动问题。 作为 PID 定义的一部分，你可以指定在进程中定义的函数，并使用函数中的通配符 * ) 指定 (或所有偏移量。 PID 提供程序要求在执行脚本时启动或运行二进制文件。

此示例命令显示与 notepad.exe 关联的 PID 中特定调用的相关信息。 使用 "调试器 [lm (列出加载的模块") ](https://docs.microsoft.com/windows-hardware/drivers/debugger/lm--list-loaded-modules-) 命令列出所有可用模块。

```dtrace
C:\Windows\system32>dtrace -ln "pid$target:ntdll:RtlAllocateHeap:entry" -c notepad.exe
   ID   PROVIDER            MODULE                          FUNCTION NAME
 5102    pid6100             ntdll                   RtlAllocateHeap entry
```

## <a name="dtrace-windows-architecture"></a>DTrace Windows 体系结构

用户通过 DTrace 命令与 DTrace 交互，后者作为 DTrace 引擎的前端。 在用户空间中 (的 DIF) 并发送到 DTrace 内核组件进行执行（有时称为 "DIF" 虚拟机），将 D 脚本编译为中间格式。 这会在 dtrace.sys 驱动程序中运行。

Traceext.sys (跟踪扩展) 是一个 Windows 内核扩展驱动程序，它允许 Windows 公开 DTrace 依赖来提供跟踪功能。 Windows 内核在 stackwalk 或内存访问过程中提供了注解，然后由跟踪扩展来实现。

![DTrace Windows 体系结构显示了与 libtrace 通信的 dtrace.exe，这与 DTrace.sys，后者会调用 Traceext.sys](images/dtrace-architecture.png)

## <a name="installing-dtrace-under-windows"></a>在 Windows 下安装 DTrace

1. 检查是否正在运行受支持的 Windows 版本。 版本18980和 Windows Server 有问必答 Preview 版本18975后，20H1 Windows 的内部版本支持 DTrace 的当前下载。 *在较早版本的 Windows 上安装此版本的 DTrace 可能导致系统不稳定，不建议这样做。*

   适用于19H1 的 DTrace 存档版本适用于 [Windows 上存档的下载 dtrace](https://www.microsoft.com/download/58091)。 请注意，不再支持此版本的 DTrace。


1. 从 Microsoft 下载中心下载 MSI 安装文件- [在 Windows 上下载 DTrace](https://www.microsoft.com/download/details.aspx?id=100441)。


2. 选择 "完全安装"。

    > [!IMPORTANT]
    > 使用 bcdedit 更改启动信息之前，你可能需要在测试电脑上暂时挂起 Windows 安全功能，如 Patchguard、BitLocker 和安全启动。
    > 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

3. 使用 bcdedit 命令在计算机上启用 DTrace。  

```cmd
bcdedit /set dtrace ON
```

当你更新到新的 Windows 预览体验版本时，你将需要再次设置 dtrace bcdedit 选项。

> [!NOTE]
> 如果你使用的是 BitLocker，请在对启动值进行更改时将其禁用。 如果不这样做，系统可能会提示你输入 BitLocker 恢复密钥。 从这种情况恢复的一种方法是启动到恢复控制台并还原 bcdedit 值 `bcdedit /set {default} dtrace on` 。 如果操作系统更新移除了值并将其添加到中，则若要恢复操作系统，请使用 bcdedit 删除值 `bcdedit /deletevalue {default} dtrace` 。 然后，禁用 BitLocker 并重新启用 dtrace `bcdedit /set dtrace ON` 。

在计算机上配置 VSM (虚拟安全模式) ，通过将 "HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\DeviceGuard\EnableVirtualizationBasedSecurity" 设置为1以启用 VSM 和安全内核，启用内核函数边界跟踪 (FBT) 。

为此，请使用 REG Add 命令，如下所示：

```cmd
REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceGuard\ /v EnableVirtualizationBasedSecurity /t REG_DWORD /d 1
```

一些 DTrace 命令使用 Windows 符号。 若要使用 Windows 符号，请创建符号目录并设置符号路径：  

```cmd
mkdir c:\symbols
set _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols 
```

有关符号路径的详细信息，请参阅 [Windows 调试器的符号路径](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)。

### <a name="using-dtrace-inside-of-a-virtual-machine"></a>在虚拟机内使用 DTrace

如果在 VM 上运行 DTrace，请在 VM 停止时，使用以下 PowerShell 命令在支持 VM 的计算机上启用嵌套虚拟化。 为正在 `<VMName>` 运行 DTrace 的 VM 提供。 以管理员身份打开 PowerShell 窗口。

```powershell
Set-VMProcessor -VMName <VMName> -ExposeVirtualizationExtensions $true
```

重新启动支持 VM 的 PC。

### <a name="validating-the-dtrace-installation"></a>验证 DTrace 安装

使用-l 选项列出活动探测。 如果 DTrace 处于活动状态，则应为 etw 事件和系统事件列出多个探测。

以管理员身份打开 Windows 命令提示符以输入 DTrace 命令。

```dtrace
C:\> dtrace -l

...

  179    syscall                                 NtLockVirtualMemory return
  180    syscall                               NtDeviceIoControlFile entry
  181    syscall                               NtDeviceIoControlFile return
  182    syscall                                 NtCreateUserProcess entry
  183    syscall                                 NtCreateUserProcess return
  184    syscall                                      NtQuerySection entry
  185    syscall                                      NtQuerySection return

...

 3161        etw 222962ab-6180-4b88-a825-346b75f2a24a           0xff_0xffffffffffffffff generic_event
 3162        etw 3ac66736-cc59-4cff-8115-8df50e39816b           0xff_0xffffffffffffffff generic_event
 3163        etw 42695762-ea50-497a-9068-5cbbb35e0b95           0xff_0xffffffffffffffff generic_event
 3164        etw 3beef58a-6e0f-445d-b2a4-37ab737bd47e           0xff_0xffffffffffffffff generic_event

...

```

如果仅列出这三个探测，则加载 DTrace.sys 驱动程序时出现问题。

```dtrace
C:\>  dtrace -l
   ID   PROVIDER            MODULE                          FUNCTION NAME
    1     dtrace                                                     BEGIN
    2     dtrace                                                     END
    3     dtrace                                                     ERROR
```

## <a name="getting-started-with-dtrace---one-line-commands"></a>DTrace 入门-一行命令

从管理员命令提示符运行这些命令即可开始。

此命令按计划显示5秒的 syscall summary。 5sec 参数指定时间段。 Exit (0) ;使命令在完成后退出到命令提示符。 使用指定的输出将 `[pid,execname] = count();` 显示进程 ID (PID) 、可执行文件名称和最后5秒的计数。

``` dtrace
C:\> dtrace -Fn "tick-5sec {exit(0);} syscall:::entry{ @num[pid,execname] = count();} "  
dtrace: description 'tick-5sec ' matched 471 probes
CPU FUNCTION
  0 | :tick-5sec

     1792  svchost.exe                                                       4
     4684  explorer.exe                                                      4
     4916  dllhost.exe                                                       4
     6192  svchost.exe                                                       4
     6644  SecurityHealth                                                    4
       92  TrustedInstall                                                    5
      504  csrss.exe                                                         5
      696  svchost.exe                                                       6
...
```

此命令汇总了3秒的计时器设置/取消调用：  

``` dtrace
C:\> dtrace -Fn "tick-3sec {exit(0);} syscall::Nt*Timer*:entry { @[probefunc, execname, pid] = count();}"
dtrace: description 'tick-3sec ' matched 14 probes
CPU FUNCTION
  0 | :tick-3sec

  NtCreateTimer                                       WmiPrvSE.exe                                            948                1
  NtCreateTimer                                       svchost.exe                                             564                1
  NtCreateTimer                                       svchost.exe                                            1276                1
  NtSetTimer2                                         svchost.exe                                            1076                1
  NtSetTimer2                                         svchost.exe                                            7080                1
  NtSetTimerEx                                        WmiPrvSE.exe                                            948                1
...  
```

### <a name="one-line-commands-that-use-symbols"></a>使用符号的一行命令

这些命令利用 Windows 符号，并要求符号路径设置为 "安装" 部分中讨论的内容。
如前文所述，使用这些命令创建一个目录并设置符号路径。

```cmd
C:\> mkdir c:\symbols
C:\> set _NT_SYMBOL_PATH=srv*C:\symbols*https://msdl.microsoft.com/download/symbols
```

此示例命令显示最常见的 NT 函数。

```dtrace
C:\> dtrace -n "fbt:nt:*Timer*:entry { @k[probefunc] = count(); } tick-5s { trunc(@k, 10);printa(@k); exit(0); }"
dtrace: description 'fbt:nt:*Timer*:entry ' matched 340 probes
CPU     ID                    FUNCTION:NAME
  0  22362                         :tick-5s
  KeCancelTimer                                                   712
  KeSetTimer2                                                     714
  HalpTimerClearProblem                                           908
  ExpSetTimerObject                                               935
  NtSetTimerEx                                                    935
  KeSetTimer                                                     1139
  KeSetCoalescableTimer                                          3159
  KeResumeClockTimerFromIdle                                    11767
  xHalTimerOnlyClockInterruptPending                            22819
  xHalTimerQueryAndResetRtcErrors                               22819
```

此命令转储 SystemProcess 内核结构。

```dtrace
C:\> dtrace -n "BEGIN {print(*(struct nt`_EPROCESS *) nt`PsInitialSystemProcess);exit(0);}"

...

   uint64_t ParentSecurityDomain = 0
    void *CoverageSamplerContext = 0
    void *MmHotPatchContext = 0
    union _PS_PROCESS_CONCURRENCY_COUNT ExpectedConcurrencyCount = {
         Fraction :20 = 0
         Count :12 = 0
        uint32_t AllFields = 0
    }
    struct _KAFFINITY_EX IdealProcessorSets = {
        uint16_t Count = 0x1
        uint16_t Size = 0x20
        uint32_t Reserved = 0
        uint64_t [32] Bitmap = [ 0x1, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 ]
    }
}
```

此命令显示过去10秒的顶层内核堆栈。

``` dtrace
C:\> dtrace -qn "profile-997hz { @[stack()] = count(); } tick-10sec { trunc(@,5); printa(@); exit(0);}"

              nt`KiDispatchInterruptContinue
              nt`KiDpcInterrupt+0x318
              nt`KiSwapThread+0x1054
              nt`KiCommitThreadWait+0x153
              nt`KeRemoveQueueEx+0x263
              nt`IoRemoveIoCompletion+0x54
              nt`NtWaitForWorkViaWorkerFactory+0x284
              nt`KiSystemServiceCopyEnd+0x35
               14

              nt`KiDispatchInterruptContinue
              nt`KiDpcInterrupt+0x318
...
```

此命令显示在启动过程中 notepad.exe 调用的顶部模块。 -C 选项运行指定的命令 ( # A0) 并在其完成后退出。

``` dtrace
C:\> dtrace -qn "pid$target:::entry { @k[probemod] = count();} tick-10s{printa(@k); exit(0);}" -c notepad.exe

  gdi32full                                                         5
  msvcp_win                                                         6
  combase                                                           7
  notepad                                                           9
  ADVAPI32                                                         10
  GDI32                                                            11
  SHELL32                                                          11
  USER32                                                           21
  win32u                                                          345
  KERNELBASE                                                     3727
  msvcrt                                                         7749
  KERNEL32                                                       9883
  RPCRT4                                                        11710
  ntdll                                                        383445

```

## <a name="see-also"></a>请参阅

[DTrace Windows 编程](dtrace-programming.md)

[DTrace ETW](dtrace-etw.md)

[DTrace 实时转储](dtrace-live-dump.md)

[DTrace Windows 代码示例](dtrace-code-samples.md)
