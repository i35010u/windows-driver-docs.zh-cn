---
title: 调试内存泄漏-DRIVER_VERIFIER_DETECTED_VIOLATION （C4）0x62
description: 驱动程序验证程序在卸载驱动程序时，如果不首先释放其所有池分配，则会生成参数1值为0x62 的 Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION。
ms.assetid: CDBE9A18-4126-4AD7-8E53-6D75DCA8B022
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6147ff25f22b1be366924c7e121172e9f5aba495
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839569"
---
# <a name="debugging-memory-leaks---driver_verifier_detected_violation-c4-0x62"></a>调试内存泄漏-检测到\_验证程序\_的驱动程序\_冲突（C4）：0x62


驱动程序[验证](driver-verifier.md)程序生成[**Bug 检查0XC4：检测到驱动程序\_验证程序\_检测到\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)与参数1的值为0x62 时，无需首先释放其所有池分配。 Unfreed 内存分配（也称为内存泄漏）是导致操作系统性能降低的常见原因。 这会使系统池分段并最终导致系统崩溃。

如果将内核调试器连接到运行[驱动程序验证](driver-verifier.md)程序的测试计算机，则当驱动程序验证器检测到冲突时，Windows 将中断调试器并显示错误的简短说明。

## <a name="debugging-memory-leaks-at-driver-unload"></a>卸载驱动程序时 > 调试内存泄漏


-   [使用！分析显示 bug 检查的相关信息](#use-analyze-to-display-information-about-the-bug-check)
-   [使用！ verifier 3 扩展命令了解池分配](#use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations)
-   [如果你具有符号，则可以在源文件中的何处发生内存分配](#if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred)
-   [检查日志中的内存分配](#examine-the-log-for-memory-allocations)
-   [修复内存泄漏](#fixing-memory-leaks)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用！分析显示 bug 检查的相关信息

与发生的任何 bug 检查一样，在控制调试器后，最好的第一步是运行[ **！分析-v**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)命令。

```
kd> !analyze -v
Connected to Windows 8 9600 x86 compatible target
Loading Kernel Symbols
.................................................................................
Loading User Symbols
.......................
Loading unloaded module list
........
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DRIVER_VERIFIER_DETECTED_VIOLATION (c4)
A device driver attempting to corrupt the system has been caught.  This is
because the driver was specified in the registry as being suspect (by the
administrator) and the kernel has enabled substantial checking of this driver.
If the driver attempts to corrupt the system, bugchecks 0xC4, 0xC1 and 0xA will
be among the most commonly seen crashes.
Arguments:
Arg1: 00000062, A driver has forgotten to free its pool allocations prior to unloading.
Arg2: 9707712c, name of the driver having the issue.
Arg3: 9c1faf70, verifier internal structure with driver information.
Arg4: 00000003, total # of (paged+nonpaged) allocations that weren't freed.
    Type !verifier 3 drivername.sys for info on the allocations
    that were leaked that caused the bugcheck.
```

[**检测到 Bug 检查 0xC4\_：\_检测到\_** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)与参数1（Arg1）值为 "0x62" 的冲突，如下所述：

检测到\_验证程序\_检测到\_冲突（C4） Arg1 Arg2 Arg3 Arg4 导致驱动程序验证程序标志0x62 驱动程序名称。
保留未释放的总分配数，包括分页池和非分页池。
卸载驱动程序时，不首先释放其池分配。 在 Windows 8.1 中，如果卸载驱动程序时未首先释放已使用[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)分配的任何工作项（[**IO\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)工作项），则也会发生此 bug 检查。 仅当[池跟踪](pool-tracking.md)选项处于活动状态时，才会发生带有此参数的 bug 检查。
指定[池跟踪](pool-tracking.md)（**verifier/flags 0x8**）。 池跟踪选项是通过标准标志（**verifier/标准**）启用的。
 

### <a name="use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations"></a>使用！ verifier 3 扩展命令了解池分配

对于此特定的错误检查，参数4（Arg4）中提供的信息是最重要的。 Arg4 显示未释放的分配数。 " [ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)" 命令的输出还显示了[ **！ verifier**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-verifier)调试器扩展命令，可用于显示这些分配的内容。 以下示例演示了 **！ verifier 3 MyDriver**命令的完整输出：

```
kd> !verifier 3 Mydriver.sys

Verify Flags Level 0x000209bb

  STANDARD FLAGS:
    [X] (0x00000000) Automatic Checks
    [X] (0x00000001) Special pool
    [X] (0x00000002) Force IRQL checking
    [X] (0x00000008) Pool tracking
    [X] (0x00000010) I/O verification
    [X] (0x00000020) Deadlock detection
    [X] (0x00000080) DMA checking
    [X] (0x00000100) Security checks
    [X] (0x00000800) Miscellaneous checks
    [X] (0x00020000) DDI compliance checking

  ADDITIONAL FLAGS:
    [ ] (0x00000004) Randomized low resources simulation
    [ ] (0x00000200) Force pending I/O requests
    [ ] (0x00000400) IRP logging
    [ ] (0x00002000) Invariant MDL checking for stack
    [ ] (0x00004000) Invariant MDL checking for driver
    [ ] (0x00008000) Power framework delay fuzzing
    [ ] (0x00040000) Systematic low resources simulation
    [ ] (0x00080000) DDI compliance checking (additional)
    [ ] (0x00200000) NDIS/WIFI verification
    [ ] (0x00800000) Kernel synchronization delay fuzzing
    [ ] (0x01000000) VM switch verification

    [X] Indicates flag is enabled


Summary of All Verifier Statistics

  RaiseIrqls           0x0
  AcquireSpinLocks     0x0
  Synch Executions     0x0
  Trims                0x0

  Pool Allocations Attempted             0x2db1a
  Pool Allocations Succeeded             0x2db1a
  Pool Allocations Succeeded SpecialPool 0x2db1a
  Pool Allocations With NO TAG           0x0
  Pool Allocations Failed                0x0

  Current paged pool allocations         0x0 for 00000000 bytes
  Peak paged pool allocations            0x0 for 00000000 bytes
  Current nonpaged pool allocations      0x3 for 00001058 bytes
  Peak nonpaged pool allocations         0x13 for 0004A4A0 bytes

## Driver Verification List


  MODULE: 0x84226b28 MyDriver.sys (Loaded)

    Pool Allocation Statistics: ( NonPagedPool / PagedPool )

      Current Pool Allocations: ( 0x00000003 / 0x00000000 )
      Current Pool Bytes:       ( 0x00001058 / 0x00000000 )
      Peak Pool Allocations:    ( 0x00000013 / 0x00000000 )
      Peak Pool Bytes:          ( 0x0004A4A0 / 0x00000000 )
      Contiguous Memory Bytes:       0x00000000
      Peak Contiguous Memory Bytes:  0x00000000

    Pool Allocations:

      Address     Length      Tag   Caller    
      ----------  ----------  ----  ----------
      0x982a8fe0  0x00000020  VMdl  0x9a3bf6ac  MyDriver!DeviceControlDispatch
      0x8645a000  0x00001008  mdrv  0x9a3bf687  MyDriver!DeviceControlDispatch
      0x9a836fd0  0x00000030  Vfwi  0x9a3bf6ed  MyDriver!GetNecessaryObjects
```

例如，驱动程序 MyDriver 有两个内存分配，一个尚未正确释放的 i/o 工作项。 每个列表显示当前分配的地址、大小、所使用的池标记，以及在其中进行分配请求的驱动程序代码中的地址。 如果为所述的驱动程序加载符号，它还将显示调用方地址旁边的函数名称。

在显示的标记中，驱动程序本身仅提供一个（用于地址0x8645a000 的分配）（**mdrv**）。 只要驱动程序验证器验证的驱动程序调用[**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)，就会使用标记**VMdl** 。 同样，每当驱动程序验证程序验证的驱动程序发出请求以使用[**IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)分配工作项时，就会使用标记**Vfwi** 。

### <a name="if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred"></a>如果你具有符号，则可以在源文件中的何处发生内存分配

为驱动程序加载符号时，如果这些符号包含行号信息，则可以使用**ln** *CallerAddress*命令来显示发出调用的行。 此输出还会显示函数中进行分配的偏移量。

```
kd> ln 0x9a3bf6ac  
d:\coding\wdmdrivers\mydriver\handleioctl.c(50)+0x15
(9a3bf660)   MyDriver!DeviceControlDispatch+0x4c   |  (9a3bf6d0)   MyDriver!DeviceControlDispatch

kd> ln 0x9a3bf687  
d:\coding\wdmdrivers\mydriver\handleioctl.c(38)+0x12
(9a3bf660)   MyDriver!DeviceControlDispatch+0x27   |  (9a3bf6d0)   MyDriver!DeviceControlDispatch

kd> ln 0x9a3bf6ed  
d:\coding\wdmdrivers\mydriver\handleioctl.c(72)+0xa
(9a3bf6d0)   MyDriver!GetNecessaryObjects+0x1d   |  (9a3bf71c)   MyDriver!GetNecessaryObjects
```

### <a name="examine-the-log-for-memory-allocations"></a>检查日志中的内存分配

启用池跟踪后，驱动程序验证器还会保留内核空间中所进行的所有内存分配的循环日志。 默认情况下，将保留最新的65536（0x10000）分配。 进行新分配时，将覆盖日志中最早的分配。 如果在发生故障之前最近进行了分配，则可以获取有关分配的其他信息，而不是如上所示，特别是在分配时内核堆栈的线程地址和帧。

可以使用命令 **！ verifier 0x80** *AddressOfPoolAllocation*访问此日志。 请注意，这会列出所有分配并在日志中释放此特定地址。 若要取消或停止显示日志历史记录，请使用键盘快捷键： **ctrl + Break** with WinDbg，使用**ctrl + C** with KD。

```
kd> !verifier 0x80 0x982a8fe0

Log of recent kernel pool Allocate and Free operations:

There are up to 0x10000 entries in the log.

Parsing 0x00010000 log entries, searching for address 0x982a8fe0.

# 

Pool block 982a8fe0, Size 00000020, Thread 9c158bc0
81b250cd nt!IovAllocateMdl+0x3d
8060e41d VerifierExt!IoAllocateMdl_internal_wrapper+0x35
81b29388 nt!VerifierIoAllocateMdl+0x22
9a3bf6ac MyDriver!DeviceControlDispatch+0x4c
9a3bf611 MyDriver!NonPNPIRPDispatch0x51
9a3bf05a MyDriver!AllIRPDispatch+0x1a
80611710 VerifierExt!xdv_IRP_MJ_DEVICE_CONTROL_wrapper+0xd0
81b3b635 nt!ViGenericDispatchHandler+0x2d
81b3b784 nt!ViGenericDeviceControl+0x18
81b24b4d nt!IovCallDriver+0x2cc
81703772 nt!IofCallDriver+0x62
8191165e nt!IopSynchronousServiceTail+0x16e
81915518 nt!IopXxxControlFile+0x3e8

kd> !verifier 0x80 0x8645a000

Log of recent kernel pool Allocate and Free operations:

There are up to 0x10000 entries in the log.

Parsing 0x00010000 log entries, searching for address 0x8645a000.

# 

Pool block 8645a000, Size 00001000, Thread 9c158bc0
8060ee4f VerifierExt!ExAllocatePoolWithTagPriority_internal_wrapper+0x5b
81b2619e nt!VerifierExAllocatePoolWithTag+0x24
9a3bf687 MyDriver!DeviceControlDispatch+0x27
9a3bf611 MyDriver!NonPNPIRPDispatch0x51
9a3bf05a MyDriver!AllIRPDispatch+0x1a
80611710 VerifierExt!xdv_IRP_MJ_DEVICE_CONTROL_wrapper+0xd0
81b3b635 nt!ViGenericDispatchHandler+0x2d
81b3b784 nt!ViGenericDeviceControl+0x18
81b24b4d nt!IovCallDriver+0x2cc
81703772 nt!IofCallDriver+0x62
8191165e nt!IopSynchronousServiceTail+0x16e
81915518 nt!IopXxxControlFile+0x3e8
81914516 nt!NtDeviceIoControlFile+0x2a

kd> !verifier 0x80 0x9a836fd0  

Log of recent kernel pool Allocate and Free operations:

There are up to 0x10000 entries in the log.

Parsing 0x00010000 log entries, searching for address 0x9a836fd0.

# 

Pool block 9a836fd0, Size 00000030, Thread 88758740
8151713d nt!IovAllocateWorkItem+0x1b
84a133d9 VerifierExt!IoAllocateWorkItem_internal_wrapper+0x29
8151b3a7 nt!VerifierIoAllocateWorkItem+0x16
9a3bf6ed MyDriver!GetNecessaryObjects+0x1d
9a3bf620 MyDriver!NonPNPIRPDispatch0x51
9a3bf05a MyDriver!AllIRPDispatch+0x1a
84a16710 VerifierExt!xdv_IRP_MJ_DEVICE_CONTROL_wrapper+0xd0
8152d635 nt!ViGenericDispatchHandler+0x2d
8152d784 nt!ViGenericDeviceControl+0x18
81516b4d nt!IovCallDriver+0x2cc
810f5772 nt!IofCallDriver+0x62
8130365e nt!IopSynchronousServiceTail+0x16e
81307518 nt!IopXxxControlFile+0x3e8
```

### <a name="fixing-memory-leaks"></a>修复内存泄漏

此驱动程序验证程序 bug 检查旨在防止驱动程序泄漏内核内存。 在每种情况下，正确的解决方法是确定任何现有的代码路径，这些路径中未释放已分配的对象并确保它们已正确释放。

[静态驱动程序验证程序](static-driver-verifier.md)是一种工具，它通过模拟各种代码路径的行使来扫描 Windows 驱动程序源代码，并报告可能的问题。 静态驱动程序验证程序是一个出色的开发时实用工具，可帮助确定这些类型的问题。

对于你可以使用的其他技术（包括不涉及驱动程序验证程序的方案），请参阅[查找内核模式的内存泄漏](https://docs.microsoft.com/windows-hardware/drivers/debugger/finding-a-kernel-mode-memory-leak)。

## <a name="related-topics"></a>相关主题


[查找内核模式内存泄漏](https://docs.microsoft.com/windows-hardware/drivers/debugger/finding-a-kernel-mode-memory-leak)

[静态驱动程序验证程序](static-driver-verifier.md)

[Windows 调试](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)

[启用驱动程序验证程序时处理 Bug 检查](https://docs.microsoft.com/windows-hardware/drivers/debugger/handling-a-bug-check-when-driver-verifier-is-enabled)

 

 






