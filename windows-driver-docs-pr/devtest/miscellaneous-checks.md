---
title: 其他检查
description: 其他检查
keywords:
- 杂项检查选项 WDK 驱动程序验证程序
- lookasides WDK 驱动程序验证程序
- 已释放内存 WDK 驱动程序验证程序
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 08500b3999e828b79e7ba2b10be5849c83370fbf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837317"
---
# <a name="miscellaneous-checks"></a>其他检查

驱动程序验证程序的 "杂项检查" 选项监视驱动程序是否存在导致驱动程序或系统崩溃的常见错误，如释放仍包含活动内核对象的内存。

具体而言，"杂项检查" 选项将查找以下不正确的驱动程序行为：

- **已释放内存中的活动工作项。** 驱动程序调用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 来释放包含使用 [**IoQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)排队的工作项的池块。

- **已释放内存中的活动资源。** 驱动程序调用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 来释放包含活动 [ERESOURCE 结构](../kernel/eresource-structures.md)的池块。 在调用 **ExFreePool** 之前，驱动程序应调用 [**EXDELETERESOURCE**](../kernel/mmcreatemdl.md)来删除 ERESOURCE 对象。

- **已释放内存中的活动后备链表列表。** 驱动程序调用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 来释放仍包含活动后备链表列表 ([**NPAGED \_ 后备链表 \_ 列表**](../kernel/eprocess.md) 或 [**分页 \_ 后备链表 \_ 列表**](../kernel/eprocess.md) 结构的池块。 在调用 **ExFreePool** 之前，驱动程序应调用 [**ExDeleteNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletenpagedlookasidelist)或 [**ExDeletePagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeletepagedlookasidelist)以删除后备链表列表。

- **Windows (ETW) 注册问题 Windows Management Instrumentation (WMI) 和事件跟踪。** 驱动程序验证程序检测到的此类问题包括：

  - 尝试在不取消注册其 WMI 回调的情况下卸载的驱动程序。

  - 尝试删除未从 WMI 中注销的设备对象的驱动程序。

  - 尝试在不注销其 ETW 内核模式提供程序的情况下卸载的驱动程序。

  - 尝试注销已取消注册的提供程序的驱动程序。

- **内核句柄错误。**  (Windows Vista 及更高版本) 启用 "杂项检查" 选项还将为系统进程启用处理跟踪，以帮助调查内核句柄泄漏和 [**Bug 检查0x93： \_ 内核 \_ 句柄无效**](../debugger/bug-check-0x93--invalid-kernel-handle.md)。 启用句柄跟踪后，内核将收集最近句柄打开和关闭操作的堆栈跟踪。 使用 **！ htrace** 调试器扩展可以在内核调试器中显示堆栈跟踪。 有关 **！ htrace** 的详细信息，请参阅 Windows 调试工具文档。

- **使用内核模式访问的用户模式句柄** 从 Windows 7 开始，在选择 "杂项检查" 选项时，驱动程序验证器还会检查对 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)的调用。 不能使用内核模式访问传递用户模式句柄。 如果发生此类操作，驱动程序验证程序将发出 Bug 检查0xC4，参数1值为0xF6。

- **UserMode 等待在内核堆栈上分配的同步对象**

    从 Windows 7 开始，驱动程序验证程序可以检测到驱动程序可以使用操作系统提供的多线程同步机制错误地使用的其他方法。

    将同步对象（如 KEVENT 结构）作为内核堆栈上的局部变量进行分配是一种常见的做法。 当进程加载到内存中时，它的线程的内核堆栈永远不会从工作集中修整或分页到磁盘。 在此类不可分页内存中分配同步对象是正确的。

    但是，当驱动程序调用 Api （如 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)或 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects) ）等待在堆栈上分配的对象时，它们必须为 API 的 *WaitMode* 参数指定 **KernelMode** 值。 当进程的所有线程都在 **UserMode** 模式下等待时，该进程将有资格换出到磁盘。 因此，如果驱动程序将 **UserMode** 指定为 *WaitMode* 参数，则只要同一进程中的每个其他线程都等待 **UserMode**，操作系统就可以交换当前进程。 将整个过程交换到磁盘上包括对其内核堆栈进行分页。 正在等待操作系统已交换的同步对象不正确。 在某一时刻，线程必须伴随，并向同步对象发出信号。 向同步对象发出信号涉及到在 IRQL = 调度 \_ 级别或更高级别处理对象的 Windows 内核。 在派单或更高级别上触摸已分页或换出内存会 \_ 导致系统崩溃。

    从 Windows 7 开始，当你选择 "杂项检查" 选项时，驱动程序验证器将检查已验证驱动程序用于在 **UserMode** 中等待的同步对象是否未在当前线程的内核堆栈上进行分配。 当驱动程序验证器检测到此类错误等待时，它会发出 [**错误检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)，参数1值为0x123。

- **内核句柄引用不正确**

    每个 Windows 进程都有一个句柄表。 您可以将句柄表作为句柄项的数组进行查看。 每个有效的句柄值都引用此数组中的有效条目。

    作为句柄的 *内核句柄* ，对系统进程的句柄表有效。 作为句柄的 *用户句柄* ，该句柄对于除系统进程外的任何进程都有效。

    在 Windows 7 中，驱动程序验证程序检测到引用不正确的内核句柄值。 如果启用了驱动程序验证程序的杂项检查选项，则这些驱动程序缺陷将报告为 [**Bug 检查0x93：无效 \_ 内核 \_ 句柄**](../debugger/bug-check-0x93--invalid-kernel-handle.md) 。 通常，这种不正确的句柄引用意味着驱动程序已关闭该句柄，但正在尝试继续使用该句柄。 此类缺陷可能会导致系统无法预测的问题，因为正在引用的句柄值可能已被另一个不相关的驱动程序使用过。

    如果内核驱动程序最近关闭了内核句柄，以后引用了关闭的句柄，则驱动程序验证程序会强制执行 bug 检查，如前文所述。 在这种情况下， [**！ htrace**](../debugger/-htrace.md) 调试器扩展的输出为关闭此句柄的代码路径提供堆栈跟踪。 使用系统进程的地址作为 **！ htrace** 的参数。 若要查找系统进程的地址，请使用 **！ process 4 0** 命令。

    从 Windows 7 开始，驱动程序验证器将检查添加到 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)。 现在禁止通过 KernelMode 访问传递用户空间句柄。 如果检测到此类组合，则驱动程序验证程序问题 [**Bug 检查0xC4：驱动程序 \_ 验证器 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)，参数1值为0xF6。

## <a name="activating-this-option"></a>激活此选项

您可以使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 "杂项检查" 选项。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

- **在命令行中**

    在命令行中，"杂项检查" 选项由第 **11 个 (0x800)** 表示。 若要激活杂项检查，请使用0x800 的标志值或将0x800 添加到标志值。 例如：

    ```console
    verifier /flags 0x800 /driver MyDriver.sys
    ```

    选项将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令，来激活和停用其他检查，无需重新启动计算机。 例如：

    ```console
    verifier /volatile /flags 0x800 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

    "杂项检查" 选项也包含在标准设置中。 例如：

    ```console
    verifier  /standard /driver MyDriver.sys
    ```

- **使用驱动程序验证器管理器**

    1. 启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。

    1. 选择 " **为代码开发人员 (创建自定义设置")**，然后单击 " **下一步**"。

    1. 选择 " **从完整列表中选择单个设置**"。

    1. 选择 " **杂项检查**"。

    "杂项检查" 功能也包含在标准设置中。 若要使用此功能，请在驱动程序验证器管理器中单击 " **创建标准设置**"。

## <a name="viewing-the-results"></a>查看结果

若要查看 "杂项检查" 选项的结果，请在内核调试器中使用 **！ verifier** 扩展。  (有关 **！ verifier** 的信息，请参阅 *Windows 调试工具* 文档。 ) 

在下面的示例中，"杂项检查" 选项检测到驱动程序在内存中正在尝试释放的活动 ERESOURCE 结构，导致 [**错误检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)。 Bug 检查0xC4 显示包括 ERESOURCE 的地址和受影响的内存。

```console
1: kd> !verifier 1

Verify Level 800 ... enabled options are:
 Miscellaneous checks enabled

Summary of All Verifier Statistics

RaiseIrqls                             0x0
AcquireSpinLocks                       0x0
Synch Executions                       0x0
Trims                                  0x0

Pool Allocations Attempted             0x1
Pool Allocations Succeeded             0x1
Pool Allocations Succeeded SpecialPool 0x0
Pool Allocations With NO TAG           0x0
Pool Allocations Failed                0x0
Resource Allocations Failed Deliberately   0x0

Current paged pool allocations         0x0 for 00000000 bytes
Peak paged pool allocations            0x0 for 00000000 bytes
Current nonpaged pool allocations      0x0 for 00000000 bytes
Peak nonpaged pool allocations         0x0 for 00000000 bytes

Driver Verification List

Entry     State           NonPagedPool   PagedPool   Module

8459ca50 Loaded           00000000       00000000    buggy.sys



**_ Fatal System Error: 0x000000c4
 (0x000000D2,0x9655D4A8,0x9655D468,0x000000B0)


        0xD2 : Freeing pool allocation that contains active ERESOURCE.
               2 -  ERESOURCE address.
               3 -  Pool allocation start address.
               4 -  Pool allocation size.
```

若要调查池分配，请将 [_ *！ pool* *](../debugger/-pool.md)调试程序扩展与池分配的起始地址9655D468。  (*2* 标志仅显示包含指定地址的池的标头信息。 禁止其他池的标头信息。 ) 

```console
1: kd> !pool 9655d468  2
Pool page 9655d468 region is Paged pool
*9655d468 size:   b0 previous size:    8  (Allocated) *Bug_
```

若要查找有关 ERESOURCE 的信息，请结合使用 [**！ ( 锁 \*)**](../debugger/-locks---kdext--locks-.md) 调试程序扩展与结构的地址一起使用。

```console
1: kd> !locks 0x9655D4A8     <<<<<- ERESOURCE @0x9655D4A8 lives inside the pool block being freed

Resource @ 0x9655d4a8    Available
1 total locks
```

你还可以使用 **kb** 调试器命令显示导致故障的调用的堆栈跟踪。 下面的示例演示堆栈，包括对驱动程序验证程序截获的 **ExFreePoolWithTag** 的调用。

```console
1: kd> kb
ChildEBP RetAddr  Args to Child
92f6374c 82c2c95a 00000003 92f68cdc 00000000 nt!RtlpBreakWithStatusInstruction
92f6379c 82c2d345 00000003 9655d468 000000c4 nt!KiBugCheckDebugBreak+0x1c
92f63b48 82c2c804 000000c4 000000d2 9655d4a8 nt!KeBugCheck2+0x5a9
92f63b6c 82e73bae 000000c4 000000d2 9655d4a8 nt!KeBugCheckEx+0x1e
92f63b88 82e78c32 9655d4a8 9655d468 000000b0 nt!VerifierBugCheckIfAppropriate+0x3c
92f63ba4 82ca7dcb 9655d468 000000b0 00000000 nt!VfCheckForResource+0x52
92f63bc8 82e7fb2d 000000b0 00000190 9655d470 nt!ExpCheckForResource+0x21
92f63be4 82e6dc6c 9655d470 92f63c18 89b6c58c nt!ExFreePoolSanityChecks+0x1fb
92f63bf0 89b6c58c 9655d470 00000000 89b74194 nt!VerifierExFreePoolWithTag+0x28
92f63c00 89b6c0f6 846550c8 846550c8 846e2200 buggy!MmTestProbeLockForEverStress+0x2e
92f63c18 82e6c5f1 846e2200 846550c8 85362e30 buggy!TdDeviceControl+0xc4
92f63c38 82c1fd81 82d4d148 846550c8 846e2200 nt!IovCallDriver+0x251
92f63c4c 82d4d148 85362e30 846550c8 84655138 nt!IofCallDriver+0x1b
92f63c6c 82d4df9e 846e2200 85362e30 00000000 nt!IopSynchronousServiceTail+0x1e6
92f63d00 82d527be 00000001 846550c8 00000000 nt!IopXxxControlFile+0x684
92f63d34 82cb9efc 0000004c 00000000 00000000 nt!NtDeviceIoControlFile+0x2a
92f63d34 6a22b204 0000004c 00000000 00000000 nt!KiFastCallEntry+0x12c
```
