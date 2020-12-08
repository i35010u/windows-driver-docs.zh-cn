---
title: SD 卡请求
description: SD 卡请求
keywords:
- SD WDK 总线，请求处理
- I/o WDK SD bus
- 请求处理 WDK SD 总线
- 同步请求 WDK SD bus
- 异步请求 WDK SD bus
- SdBusSubmitRequest
- SdBusSubmitRequestAsync
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d61cebc02e78f7a777efe9c6dabde4e68e333848
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831113"
---
# <a name="sd-card-requests"></a>SD 卡请求


安全数字 (SD 后) 卡设备驱动程序已打开并初始化 SD bus 驱动程序的接口，它可以提交请求。 可以通过两种方法来提交请求：通过 [**SdBusSubmitRequest**](/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest) 例程同步，并通过 [**SdBusSubmitRequestAsync**](/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequestasync) 例程进行异步处理。 这两个例程均由 SD 总线库导出 (*sdbus*) 。

同步请求例程使用两个参数：接口上下文和请求数据包。

<a href="" id="interface-context"></a>**接口上下文**  
在使用 [**SdBusOpenInterface**](/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbusopeninterface)打开 SD 接口后，设备驱动程序从 [**SDBUS \_ 接口 \_ 标准**](/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))结构的 **上下文** 成员检索接口上下文。 每当驱动程序调用接口中的方法时，该驱动程序都必须传递此上下文信息。

<a href="" id="request-packet"></a>**请求数据包**  
设备驱动程序必须分配和初始化 [**SDBUS \_ 请求 \_ 数据包**](/previous-versions/windows/hardware/drivers/ff537931(v=vs.85)) 结构。 此结构指定请求函数和请求的其他特征。

由于 **SdBusSubmitRequest** 是同步的，因此不会返回 "挂起" 状态 \_ 。 设备驱动程序在 &lt; 调用此例程时，必须以 IRQL 调度 \_ 级别运行。

异步请求例程使用以下五个参数：接口上下文、请求数据包、IRP、指向完成例程的指针和完成上下文。

<a href="" id="interface-context"></a>**接口上下文**  
此参数与用于同步事例的相同名称的参数相同。

<a href="" id="request-packet"></a>**请求数据包**  
此参数与用于同步事例的相同名称的参数相同。

<a href="" id="irp"></a>**IRP**  
此参数包含设备驱动程序已分配的 IRP，或包含驱动程序从驱动程序堆栈中的驱动程序接收的 IRP。 IRP 用作请求的运营商。

<a href="" id="completion-routine"></a>**完成例程**  
此参数为 IRP 参数中提供的 IRP 保存 [**IoCompletion**](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。

<a href="" id="user-context"></a>**用户上下文**  
此参数保存一个指向用户上下文数据的指针，系统会将该指针传递到完成例程参数中指定的完成例程。

当设备驱动程序 &lt; \_ 调用 **SdBusSubmitRequestAsync** 例程时，必须以 IRQL = 调度级别运行。 **SdBusSubmitRequest** 是分配其自己的 IRP 并调用 **SdBusSubmitRequestAsync** 的包装器。 提供此方法是为了方便驱动程序编写器。

以下各节提供了一些代码示例，这些代码示例演示了设备驱动程序如何提交 SD 请求的两个主要类别：有关不同请求的说明，请参阅 [**SD \_ REQUEST \_ FUNCTION**](/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)。

## <a name="secure-digital-sd-property-requests"></a> (SD) 属性请求的安全数字


安全数字 (SD) 卡驱动程序使用属性请求来读取或设置卡属性。 例如，SD 卡驱动程序可能会读取属性，以确定 SD 卡上的写保护开关是否处于锁定位置，或者多功能 SDIO 卡上特定函数的驱动程序是否可以请求总线驱动程序分配给它所管理的函数的编号。

下面的代码示例演示了多功能卡上某个函数的驱动程序如何从总线驱动程序请求其功能号：

```cpp
 sdrp = ExAllocatePool(NonPagedPool, 
 sizeof(SDBUS_REQUEST_PACKET));
 if (!sdrp) {
 return STATUS_INSUFFICIENT_RESOURCES;
 }
 RtlZeroMemory(sdrp, sizeof(SDBUS_REQUEST_PACKET));
 sdrp->RequestFunction = SDRF_GET_PROPERTY;
 sdrp->Parameters.GetSetProperty.Property = 
 SDP_FUNCTION_NUMBER;
 sdrp->Parameters.GetSetProperty.Buffer = 
 &pDevExt->FunctionNumber;
 sdrp->Parameters.GetSetProperty.Length = 
 sizeof(pDevExt->FunctionNumber);
 status = SdBusSubmitRequest (pDevExt->BusInterface.Context,sdrp);
 ExFreePool(sdrp);
 if (!NT_SUCCESS(status)) {
 return status;
 }
```

在此代码示例中，设备驱动程序初始化 SD bus 请求数据包 [**SDBUS \_ 请求 \_ 数据包**](/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))，并将其传递给 [**SdBusSubmitRequest**](/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest)。 完全初始化的请求数据包具有以下特征：

<a href="" id="type-of-the-request"></a>**请求的类型**  
此代码示例 \_ \_ 在请求数据包的 **RequestFunction** 成员中指定 SDRF GET 属性请求，指示总线驱动程序从卡中检索属性。 有关 SDRF \_ GET 属性请求的说明 \_ ，请参阅 [**SD \_ 请求 \_ 函数**](/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)。

<a href="" id="property-to-retrieve"></a>**要检索的属性**  
此代码示例 \_ \_ 在请求数据包的 **GetSetProperty** 成员中指定 SDP 函数编号属性，该属性指示总线驱动程序检索 "函数编号" 属性的内容。 有关 SDP \_ 函数编号属性的说明 \_ ，请参阅 [**SDBUS \_ 属性**](/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sdbus_property)。

<a href="" id="property-contents-and-length"></a>**属性内容和长度**  
此代码示例将指针放置在设备扩展

请求数据包的 **GetSetProperty** 成员。 总线驱动程序会将函数编号存储在此位置。 示例代码还将此缓冲区的大小存储在请求数据包的 **GetSetProperty** 成员中。

## <a name="secure-digital-sd-device-command-requests"></a>安全数字 (SD) 设备命令请求


驱动程序使用安全数字 (SD) 卡命令请求将命令发送到 SD 设备。 SD 命令的协议是在 *安全数字卡* 规范中定义的。 驱动程序可以在 [**IRP \_ MN \_ 启动 \_ 设备**](../kernel/irp-mn-start-device.md) irp 成功完成后随时发送命令请求。

本部分包含两个代码示例：一个命令请求，该请求使用直接 i/o 从 SD 卡的注册读取一个字节的数据，并使用扩展 i/o 将更多的数据写入 SD 卡。 第二部分中的说明取决于第一个部分，因此读者应该在学习第二部分之前研究第一部分：

[使用的安全数字请求](/previous-versions/windows/hardware/drivers/ff538051(v=vs.85))

[使用扩展 i/o 的安全数字请求](/previous-versions/windows/hardware/drivers/ff538055(v=vs.85))

 

