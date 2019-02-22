---
title: 调试内存泄漏问题-DRIVER_VERIFIER_DETECTED_VIOLATION (C4) 0x62
description: 驱动程序验证程序将生成将 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION Bug 检查的 0x62 不首先释放其池分配的所有驱动程序的卸载时的参数 1 值。
ms.assetid: CDBE9A18-4126-4AD7-8E53-6D75DCA8B022
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01151f9b50e7e8a10e8f4e8a88a16c233bb10243
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524600"
---
# <a name="debugging-memory-leaks---driververifierdetectedviolation-c4-0x62"></a>调试内存泄漏的驱动程序\_VERIFIER\_检测到\_冲突 (C4):0x62


[Driver Verifier](driver-verifier.md)生成[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) 0x62 驱动程序时但未事先卸载的参数 1 值释放所有其池分配。 未释放的内存分配 （也称为内存泄漏） 是降低的操作系统性能的一个常见原因。 这些可以片断系统池，并最终导致系统崩溃。

内核调试程序连接到运行的测试计算机后[Driver Verifier](driver-verifier.md)，如果驱动程序验证程序检测到冲突，Windows 中断到调试器并显示错误的简短说明。

## <a name="debugging-memory-leaks-at-driver-unload"></a>> 在驱动程序卸载调试内存泄漏


-   [使用 ！ 分析以显示 bug 检查有关的信息](#use-analyze-to-display-information-about-the-bug-check)
-   [使用 ！ verifier 3 扩展命令找出有关池分配](#use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations)
-   [如果您拥有符号可以找到在源文件中的内存分配发生的位置](#if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred)
-   [检查日志中的内存分配](#examine-the-log-for-memory-allocations)
-   [修复内存泄漏](#fixing-memory-leaks)

### <a name="use-analyze-to-display-information-about-the-bug-check"></a>使用 ！ 分析以显示 bug 检查有关的信息

最佳的第一步是运行后可以控制在调试器中出现任何错误检查，与一样[ **！ 分析-v** ](https://msdn.microsoft.com/library/windows/hardware/ff562112)命令。

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

一个[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) 0x62 的值，如下所示描述与参数 1 (Arg1):

驱动程序\_VERIFIER\_检测到\_冲突 (C4) Arg1 Arg2 Arg3 了 Arg4 原因 Driver Verifier 标志 0x62 的驱动程序名称。
已不释放，包括分页和非分页池的分配总保留的数。
该驱动程序正在卸载不首先释放其池分配。 在 Windows 8.1，此 bug 检查如果也会出现第一个释放任何工作项的情况下卸载该驱动程序 ([**IO\_工作项**](https://msdn.microsoft.com/library/windows/hardware/ff550679)) 它必须与分配[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)。 使用此参数的 bug 检查时才会发生时[池跟踪](pool-tracking.md)选项处于活动状态。
指定[池跟踪](pool-tracking.md)(**verifier /flags 0x8**)。 使用标准标志启用池跟踪选项 (**verifier /standard** )。
 

### <a name="use-the-verifier-3-extension-command-to-find-out-about-the-pool-allocations"></a>使用 ！ verifier 3 扩展命令找出有关池分配

对于此特定的错误检查，参数 4 (了 Arg4) 中提供的信息是最重要的。 了 Arg4 显示的未释放的分配数。 输出[ **！ 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)命令还显示了[ **！ verifier** ](https://msdn.microsoft.com/library/windows/hardware/ff565591)调试器可用于显示内容的扩展命令这些分配的。 完整的输出 **！ verifier 3 MyDriver.sys**命令显示在下面的示例：

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

在示例中，该驱动程序，MyDriver.sys，具有两个内存分配和一个没有被正确释放的 I/O 工作项。 每个列表的请求分配了驱动程序代码中显示当前分配、 大小、 使用的池标记和地址的地址。 如果符号为有问题的驱动程序加载，它还将显示函数的调用方地址旁边的名称。

显示的标记，只有一个 （适用于在地址 0x8645a000 分配） 提供的驱动程序本身 (**mdrv**)。 标记**VMdl** Driver Verifier 正在验证的驱动程序进行调用时，将使用[ **IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)。 同样，标记**Vfwi** Driver Verifier 正在验证的驱动程序发出请求以分配工作项使用时，将使用[ **IoAllocateWorkItem**](https://msdn.microsoft.com/library/windows/hardware/ff548276)。

### <a name="if-you-have-symbols-you-can-locate-where-in-the-source-files-the-memory-allocations-occurred"></a>如果您拥有符号可以找到在源文件中的内存分配发生的位置

在加载符号时驱动程序，如果这些符号包含行号信息，可以使用**ln** *CallerAddress*命令，以显示行调用了。 此输出还会进行分配的函数中显示偏移量。

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

驱动程序验证程序也会启用跟踪的池时在内核空间中所做的所有内存分配的循环日志。 默认情况下，最新 65536 (0x10000) 进行分配。 进行新的分配，在日志中最早的分配将被覆盖。 如果最近在崩溃前进行分配，它可以获取有关在分配的时间比上面，尤其是线程地址和内核堆栈帧显示分配的其他信息。

可以使用命令访问此日志 **！ verifier 0x80** *AddressOfPoolAllocation*。 请注意这将列出所有分配并释放日志中的此特定的地址。 若要取消或停止显示日志历史记录，使用键盘快捷方式：**Ctrl + Break**使用 WinDbg 和**Ctrl + C**与 KD。

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

此驱动程序验证程序 bug 检查旨在防止驱动程序内核内存泄漏。 每种情况下，正确的解决方法是识别任何现有的代码路径，不会释放分配的对象，并确保它们正确释放。

[Static Driver Verifier](static-driver-verifier.md)是一个工具，扫描 Windows 驱动程序的源代码并通过模拟的各种代码路径执行报告可能存在的问题。 Static Driver Verifier 是一个很好的开发时间实用程序，以帮助识别这些类型的问题。

有关其他方法可用，包括的方案，其中不涉及驱动程序验证程序，请参阅[查找内核模式内存泄漏](https://msdn.microsoft.com/library/windows/hardware/ff545403)。

## <a name="related-topics"></a>相关主题


[查找内核模式内存泄漏](https://msdn.microsoft.com/library/windows/hardware/ff545403)

[Static Driver Verifier](static-driver-verifier.md)

[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)

[处理 Bug 检查时驱动程序验证程序已启用](https://msdn.microsoft.com/library/windows/hardware/hh450984)

 

 






