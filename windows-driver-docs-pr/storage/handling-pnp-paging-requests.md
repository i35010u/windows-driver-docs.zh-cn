---
title: 处理 PnP 分页请求
description: 处理 PnP 分页请求
keywords:
- 存储筛选器驱动程序 WDK、PnP
- 筛选器驱动程序 WDK 存储，PnP
- SFD WDK 存储，PnP
- PnP WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 293fcc2bde3e4c1b688255a819cc050269355ad1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804533"
---
# <a name="handling-pnp-paging-requests"></a>处理 PnP 分页请求


## <span id="ddk_handling_pnp_paging_requests_kg"></span><span id="DDK_HANDLING_PNP_PAGING_REQUESTS_KG"></span>


存储筛选器驱动程序必须使用 Irp [**\_ MJ Pnp (irp MJ \_ pnp**](../kernel/irp-mj-pnp.md)处理 pnp 寻呼请求，并将 **UsageNotification** 设置为 **DeviceUsageTypePaging**) 如果它正在筛选的函数驱动程序处理此 IRP。 [**\_ \_ \_ \_**](../kernel/irp-mn-device-usage-notification.md)

必须将以下项添加到筛选器的 DeviceExtension：

ULONG PagingCount;

KEVENT PagingCountEvent;

收到 PnP 寻呼请求后，存储筛选器驱动程序必须更新筛选器中的 PagingCount 和 **\_ \_ PAGABLE** 位的设置。 更新 " **\_ \_ PAGABLE** " 位的时间取决于是否设置或清除该位。 如果 IRP 指示应该设置位，则筛选器驱动程序必须在将 IRP 向下转发到驱动程序堆栈 *之前* 对其进行设置。 但如果 IRP 指出应清除该位，则筛选器驱动程序不应立即清除该位。 它必须首先转发 IRP，并等待较低的驱动程序返回其状态，并仅在较低的驱动程序返回 **状态为 \_ 成功** 时清除此位。

下面跟踪存储筛选器驱动程序执行的操作流。 请参阅大纲下紧下方的伪代码示例，以查看 C 代码中此大纲的表示形式：

A. 验证设备是否已启动。 否则，将失败， **状态为 " \_ 设备 \_ 未 \_ 就绪**"。

B. 在 PagingCountEvent (KeWaitForSingleObject ( PagingCountEvent 上同步，) # A3。

C. 如果删除最后一个寻呼设备 ( (！ **UsageNotification. InPath** &&  (PagingCount = = 1) ) then
1.  将本地布尔值设置为 **TRUE**，并

2.  如果在筛选器中未设置 " **执行 \_ 电源 \_ 浪涌** " 位，则设置 " **do \_ power \_ PAGABLE** " 位。

    下面说明了为何必须在 PAGABLE 中设置 **DO \_ POWER \_** 位，而不是在上移：

    电源要求状态如果任何较低的设备对象设置了 " **DO \_ power \_ PAGABLE** " 位，则所有更高级别的驱动程序都必须执行相同操作。 如果筛选器驱动程序在发送寻呼请求 IRP 之前未能设置 **DO \_ POWER \_ PAGABLE** ，则可能会违反此条件，如下所示：

    假设筛选器驱动程序不在其筛选器中设置 " **do \_ POWER \_ PAGABLE** " 位，然后将寻呼请求 IRP 转发给驱动程序堆栈中其下的驱动程序。 接下来，请注意，较低的驱动程序会自行设置 **do \_ POWER \_ PAGABLE** 位。 最后，假设在筛选器驱动程序完成 IRP 之前，会发生电源 IRP。 此时，将在筛选器中清除 **do \_ POWER \_ PAGABLE** 位，但会在较低级别的驱动程序中进行设置，从而导致系统崩溃。

    在将分页请求按堆栈向下移动之前，可以安全地设置 " **DO \_ POWER \_ PAGABLE** " 位，因为筛选器驱动程序的设备上不再有活动的分页文件，因此不会对其进行分页 i/o。 如果删除此分页文件的请求成功，则将完成筛选器驱动程序。 如果请求失败，筛选器驱动程序可以通过在完成 IRP 之前清除 **DO \_ POWER \_ PAGABLE** bit 来还原其标志的原始状态。 由于分页文件请求将进行序列化，因此，在筛选器驱动程序最后修改此位后，某些其他线程会修改此位。

D. 将 IRP 同步转发到更低的驱动程序。

E. 如果 IRP 成功完成，则

1.  调用 IoAdjustPagingPathCount ( # B0 PagingCount， **UsageNotification InPath**) 递增或递减 PagingCount。 IoAdjustPagingPathCount 对 PagingCount 执行 InterlockedIncrement 或 InterlockedDecrement，具体取决于 **UsageNotification.** InPath 中的值。 如果值为 **TRUE** ，则指示正在添加页面文件，因此递增 PagingCount;如果值为 **FALSE** ，则表示正在删除页面文件，因此减少了 PagingCount。

2.  如果 **InPath** 为 **TRUE**，则会添加一个分页文件，因此，请清除 " **执行 \_ POWER \_ PAGABLE** " 位。

F. 否则，如果 IRP 失败，

1.  检查本地布尔值，查看筛选器中是否设置了 **\_ \_ PAGABLE** 。

2.  如果按下了 **\_ \_ PAGABLE** ，请将其清除。

G. 结束同步 (KeSetEvent (PagingCountEvent，... ) # A3。

### <a name="span-idpseudocode_examplespanspan-idpseudocode_examplespanpseudocode-example"></a><span id="pseudocode_example"></span><span id="PSEUDOCODE_EXAMPLE"></span>伪代码示例

下面的代码示例中的字母 (*//A*，) *//B* 等标记的部分映射到上述大纲的字母。

```cpp
case DeviceUsageTypePaging: { 
    BOOLEAN setPageable = FALSE; 
    BOOLEAN addPageFile = irpStack -> 
                          Parameters.UsageNotification.InPath; 
 
 // A 
    if((addPageFile) && 
        (extension -> CurrentPnpState != 
        IRP_MN_START_DEVICE)) { 
            status = STATUS_DEVICE_NOT_READY; 
            break; 
        } 
 // B 
    KeWaitForSingleObject(&commonExtension -> PagingCountEvent, 
                                    Executive, KernelMode, 
                                    FALSE, NULL); 
 // C 
    if (!addPageFile && commonExtension -> PagingCount == 1 ) { 
        // The last paging file is no longer active.
        // Set the DO_POWER_PAGABLE bit before 
        // forwarding the paging request down the 
        // stack.
        if (!(DeviceObject->Flags & DO_POWER_INRUSH)) { 
            DeviceObject->Flags |=             DO_POWER_PAGABLE; 
            setPageable = TRUE; 
        ) 
    ) 
 // D 
        status = ForwardIrpSynchronous(commonExtension, Irp); 
 // E
        if (NT_SUCCESS(status)) { 
            IoAdjustPagingPathCount(&commonExtension -> PagingCount, 
                                    addPageFile); 
        if (addPageFile && commonExtension -> PagingCount == 1) { 
            // Once the lower device objects have 
            // succeeded the addition of the paging 
            // file, it is illegal to fail the 
            // request. It is also the time to 
            // clear the Filter DO's 
            //DO_POWER_PAGABLE flag.
 
            DeviceObject->Flags &= ~DO_POWER_PAGABLE; 
            } 
        } else { 
 // F 
        if (setPageable == TRUE) { 
            DeviceObject->Flags &= ~DO_POWER_PAGABLE; 
            setPageable = FALSE; 
        } 
    } 
 // G 
        KeSetEvent(&commonExtension->PagingCountEvent, 
                                    IO_NO_INCREMENT, FALSE); 
                                    break;
    } *Do not use or delete the last paragraph mark. It maintains the template setup and formats.
```

 

