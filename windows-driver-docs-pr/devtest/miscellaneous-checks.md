---
title: 其他检查
description: 其他检查
ms.assetid: 4d7b14ae-5a3a-49b4-9678-6527cbacc4d4
keywords:
- 杂项检查选项 WDK Driver Verifier
- lookasides WDK Driver Verifier
- 已释放的内存 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c65a1032595ea03bc0c32ab505865dff2dd9622
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354760"
---
# <a name="miscellaneous-checks"></a>其他检查


驱动程序验证程序的杂项检查选项可监视会导致驱动程序或系统崩溃，如释放内存仍包含活动内核对象的常见错误的驱动程序。

具体而言，杂项检查选项中查找以下不正确的驱动程序行为：

-   **已释放的内存中的活动工作项。** 驱动程序调用[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)若要释放包含工作项排队等待的使用的池块[ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)... （此检查启用默认情况下，在 Windows Server 2003 的内部版本中）。

-   **已释放的内存中的活动资源。** 驱动程序调用[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)来释放包含活动的池块[ERESOURCE 结构](https://docs.microsoft.com/windows-hardware/drivers/kernel/eresource-structures)。 该驱动程序应调用[ **ExDeleteResource** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mmcreatemdl)删除 ERESOURCE 对象之前调用**ExFreePool**。

-   **中的活动的后备链列表已释放的内存。** 驱动程序调用[ **ExFreePool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)若要释放的池块仍包含 active 后备链列表 ([**NPAGED\_后备链\_列表**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)或[ **PAGED\_后备链\_列表**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构。 该驱动程序应调用[ **ExDeleteNPagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletenpagedlookasidelist)或[ **ExDeletePagedLookasideList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exdeletepagedlookasidelist)删除后备链列表的步骤然后再调用**ExFreePool**。

-   **Windows Management Instrumentation (WMI) 和事件跟踪 Windows (ETW) 注册问题。** 检测到驱动程序验证程序的此类问题包括：
    -   尝试卸载而无需取消注册其 WMI 回调驱动程序。
    -   尝试删除尚未从 WMI 中取消注册的设备对象驱动程序。
    -   尝试卸载而无需取消注册其 ETW 内核模式提供程序驱动程序。
    -   尝试注销提供程序已注销驱动程序。
-   **内核处理错误。** （Windows Vista 和更高版本）启用杂项检查选项还将启用对系统进程，以帮助调查内核句柄泄漏的句柄跟踪并[ **Bug 检查 0x93:无效\_内核\_处理**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x93--invalid-kernel-handle)。 句柄在启用跟踪，内核将收集的堆栈跟踪为最新的句柄打开和关闭操作。 可以使用在内核调试器中显示堆栈跟踪 **！ htrace**调试器扩展。 有关详细信息 **！ htrace**，请参阅有关 Windows 调试工具文档。

-   **用户模式下使用内核模式访问的句柄**从 Windows 7 中，选择其他检查选项时，驱动程序验证程序还会检查在调用[ **ObReferenceObjectByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle). 您不能传递与内核模式访问的用户模式下句柄。 发生此类操作时，驱动程序验证程序发出 Bug 检查 0xC4、 0xF6 的参数 1 值。

-   **用户模式等待内核堆栈上分配的同步对象**

    从 Windows 7 开始，驱动程序验证工具可以检测驱动程序未正确使用操作系统提供的多线程处理同步机制的其他方式。

    作为内核堆栈上的本地变量分配了同步对象，如 KEVENT 结构是一种常见做法。 虽然进程加载到内存中，其线程的内核堆栈是永远不会从工作集修整或分页输出到磁盘。 分配了此类不可分页的内存中的同步对象是正确的。

    但是，在驱动程序调用 Api 如[ **KeWaitForSingleObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)或[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)等待一个对象，它在堆栈上分配，它们必须指定**KernelMode** api 的值*WaitMode*参数。 当进程的所有线程中都等待**UserMode**模式下，进程变得可换出到磁盘。 因此，如果指定的驱动程序**UserMode**作为*WaitMode*参数，操作系统可以换出当前进程，只要在同一进程中的每个其他线程正在等待作为**UserMode**、 过。 换出到磁盘的整个过程包括分页出其内核堆栈。 等待同步对象的操作系统具有换出不正确。 在某些时候线程必须这会发出信号的同步对象。 发出信号的同步对象涉及 Windows 内核操作的对象在 IRQL = 调度\_级别或更高版本。 触摸调出或换出内存在调度\_级别或更高版本会导致系统崩溃。

    在 Windows 7 中，从开始，选择杂项检查选项时，驱动程序验证工具将检查同步对象中等待，使用已验证的驱动程序**UserMode**在当前线程的内核上未分配堆栈。 当驱动程序验证程序检测到此类的不正确的等待时，它会发出[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)，0x123 的参数 1 值。

-   **不正确的内核句柄的引用**

    每个 Windows 进程有一个句柄表。 您可以将句柄表视为的句柄项数组。 每个有效的句柄值是指此数组中的有效项。

    一个*内核句柄*作为对系统进程的句柄表有效的句柄。 一个*用户句柄*作为有效的除系统进程的任何进程的句柄。

    在 Windows 7 中，驱动程序验证程序检测到尝试引用内核处理不正确的值。 这些驱动程序缺陷报告为[ **Bug 检查 0x93:无效\_内核\_处理**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0x93--invalid-kernel-handle)如果启用驱动程序验证工具杂项检查选项。 通常这种不正确的句柄引用意味着该驱动程序已关闭该句柄，但尝试继续使用它。 这种缺陷可能会导致不可预知的系统遇到问题，因为所引用的句柄值可能已重用已由另一个不相关的驱动程序。

    如果内核驱动程序具有最近解决的内核句柄和更高版本引用已关闭句柄，驱动程序验证程序将强制错误检查，如前面所述。 在本例中的输出[ **！ htrace** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-htrace)调试器扩展提供关闭此句柄的代码路径的堆栈跟踪。 使用系统过程的地址的参数作为 **！ htrace**。 若要查找系统进程的地址，请使用 **！ 处理 4 0**命令。

    从 Windows 7 开始，驱动程序验证程序将添加到复选[ **ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)。 现在，这种行为来传递具有 KernelMode 访问权限的用户空间句柄。 如果检测到这样的结合，则驱动程序验证程序会发出[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)，0xF6 的参数 1 值。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的其他检查选项。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，由表示杂项检查选项**位 11 (0x800)** 。 若要激活其他检查，使用 0x800 标志值，或将 0x800 添加到标志值。 例如：

    ```
    verifier /flags 0x800 /driver MyDriver.sys
    ```

    在下一次启动后，选项将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，还可以激活并停用而无需重启计算机，通过添加其他检查 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x800 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    杂项检查选项也包含在标准设置。 例如：

    ```
    verifier  /standard /driver MyDriver.sys
    ```

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择**杂项检查**。

    杂项检查功能也包含在标准设置。 若要使用此功能，驱动程序验证程序管理器中，单击**创建标准设置**。

### <a name="span-idviewingtheresultsspanspan-idviewingtheresultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>查看结果

若要查看其他检查选项的结果，请使用 **！ verifier**内核调试程序中的扩展。 (有关 **！ verifier**，请参阅*对于 Windows 调试工具*文档。)

在以下示例中，杂项检查选项检测到驱动程序已尝试释放，内存中的 active ERESOURCE 结构导致[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc4--driver-verifier-detected-violation)。 Bug 检查 0xC4 显示内容包括 ERESOURCE 和受影响的内存的地址。

```
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



*** Fatal System Error: 0x000000c4
 (0x000000D2,0x9655D4A8,0x9655D468,0x000000B0)


        0xD2 : Freeing pool allocation that contains active ERESOURCE.
               2 -  ERESOURCE address.
               3 -  Pool allocation start address.
               4 -  Pool allocation size.
```

若要调查的池分配，请使用[ **！ 池**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-pool)调试器扩展与池分配，9655D 468 的起始地址。 ( *2*标志显示池，其中包含指定的地址标头信息。 其他池的标头信息已取消显示。）

```
1: kd> !pool 9655d468  2
Pool page 9655d468 region is Paged pool
*9655d468 size:   b0 previous size:    8  (Allocated) *Bug_
```

若要查找有关 ERESOURCE 的信息，请使用[ **！ 锁 (！ kdext\*.locks)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-locks---kdext--locks-)调试器扩展与结构的地址。

```
1: kd> !locks 0x9655D4A8     <<<<<- ERESOURCE @0x9655D4A8 lives inside the pool block being freed

Resource @ 0x9655d4a8    Available
1 total locks
```

此外可以使用**kb**调试器命令，以显示导致失败的调用堆栈跟踪。 下面的示例显示了堆栈，包括对**ExFreePoolWithTag**截获该驱动程序验证程序。

```
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

 

 





