---
title: 处理分页请求即插即用
description: 处理分页请求即插即用
ms.assetid: c30c70d9-69c6-42d7-ae69-9c2421ba1d53
keywords:
- 存储筛选器驱动程序 WDK，即插即用
- 筛选驱动程序 WDK 存储，即插即用
- SFD WDK 存储，即插即用
- 即插即用 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15721b5b747f14fbc7a606863f24f5294d811774
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519311"
---
# <a name="handling-pnp-paging-requests"></a>处理分页请求即插即用


## <span id="ddk_handling_pnp_paging_requests_kg"></span><span id="DDK_HANDLING_PNP_PAGING_REQUESTS_KG"></span>


存储筛选器驱动程序必须处理分页请求即插即用 ([**IRP\_MJ\_PNP** ](https://msdn.microsoft.com/library/windows/hardware/ff550772)与[ **IRP\_MN\_设备\_使用情况\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff550841)并**Parameters.UsageNotification.Type**设置为**DeviceUsageTypePaging**) 如果所筛选的功能驱动程序处理此 IRP。

必须将以下各项添加到筛选器执行的操作的 DeviceExtension:

ULONG PagingCount;

KEVENT PagingCountEvent;

收到即插即用分页请求时，存储筛选器驱动程序必须更新 PagingCount 和的设置**做\_电源\_PAGABLE**比以筛选器执行。 更新的计时**做\_电源\_PAGABLE**位取决于是否正在该位设置或清除。 如果 IRP 指示应设置的位，则筛选器驱动程序必须将它*之前*转发驱动程序堆栈的下层 IRP。 但如果 IRP 指示应清除位，则筛选器驱动程序应立即清除的位。 必须先将转发 IRP，然后等待较低的驱动程序返回其状态并清除的位低级驱动程序返回时，才**状态\_成功**。

以下跟踪存储筛选器驱动程序所采取的操作流。 请参阅下面的轮廓，若要查看此大纲 C 代码中的表示形式的伪代码示例：

A. 验证设备已启动。 如果不是，因**状态\_设备\_不\_准备**。

B. 同步 PagingCountEvent (KeWaitForSingleObject (PagingCountEvent，...))。

C. 如果删除最后一个分页设备 (（！ **Parameters.UsageNotification.InPath** & & (PagingCount = = 1)) 然后
1.  将本地的布尔值设置为 **，则返回 TRUE**，和

2.  如果**做\_电源\_浪涌**位不是设置在筛选器执行操作，则设置**执行\_POWER\_PAGABLE**位。

    下面解释了为什么**做\_电源\_PAGABLE**位必须设置下的方式，而不用于方法：

    电源要求指出，如果任何降低设备对象集**做\_电源\_PAGABLE**位，所有更高级别的驱动程序必须执行相同操作。 如果筛选器驱动程序无法设置**做\_电源\_PAGABLE** bit 分页请求 IRP 堆栈在发送之前，它可能违反了这种情况，如下所示：

    筛选器驱动程序不会设置假设**做\_POWER\_PAGABLE**转发到其下的驱动程序堆栈中的驱动程序的分页请求 IRP 之前在其筛选器执行位。 下一步假设较低的驱动程序设置**做\_电源\_PAGABLE**位在其自身执行操作。 最后，假设的 IRP 完成之前由筛选器驱动程序 IRP 发生的幂。 此时，**做\_电源\_PAGABLE**位会清除在筛选器执行，但将设置中执行操作的较低级驱动程序，从而导致系统崩溃。

    则可以安全地设置**做\_电源\_PAGABLE**位转发堆栈的下层，分页请求之前，因为已不再在筛选器驱动程序的设备，并因此没有更多分页 I/O 活动的页面文件将在它发生。 如果要删除此分页文件的请求成功，则会执行筛选器驱动程序。 如果请求失败，筛选器驱动程序可以通过只需清除还原其标志的原始状态**做\_电源\_PAGABLE** IRP 之前位。 分页文件请求序列化，因为没有的一些其他线程将已修改此位因为筛选器驱动程序上次修改存在风险。

D. 以同步方式将转发到较低的驱动程序 IRP。

E。 如果 IRP 将成功完成，然后

1.  调用 IoAdjustPagingPathCount (& PagingCount， **Parameters.UsageNotification.InPath**) 要递增或递减 PagingCount。 IoAdjustPagingPathCount 执行 InterlockedIncrement 或根据中的值 PagingCount InterlockedDecrement **Parameters.UsageNotification.InPath**。 值为 **，则返回 TRUE**指示分页文件被添加，因此，增量 PagingCount; 如果值为**FALSE**指示正在分页文件中删除，因此递减 PagingCount。

2.  如果**Parameters.UsageNotification.InPath**是**TRUE**，添加了，因此清除的分页文件**执行\_POWER\_PAGABLE**位。

F. 否则，如果 IRP 失败，则

1.  检查本地的布尔值，以查看是否**做\_电源\_PAGABLE**已设置在方式上的筛选器执行操作。

2.  如果**做\_电源\_PAGABLE**已设置的方式，将其清除。

G. 结束同步 (KeSetEvent (PagingCountEvent，...))。

### <a name="span-idpseudocodeexamplespanspan-idpseudocodeexamplespanpseudocode-example"></a><span id="pseudocode_example"></span><span id="PSEUDOCODE_EXAMPLE"></span>伪代码示例

部分标记为按字母 (*//A*， *//B*等) 在上面所述的字母到下面的代码示例图中。

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
            // clear the Filter DO&#39;s 
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

 

 




