---
title: SD 卡请求
description: SD 卡请求
ms.assetid: 3c04573a-5fe7-4332-b899-5aff3234f1ad
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
ms.openlocfilehash: cc4a7e4276bb124113f5b1ae34b78ee9cd156948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842458"
---
# <a name="sd-card-requests"></a>SD 卡请求


安全数字（SD）卡设备驱动程序打开并初始化 SD bus 驱动程序的接口后，它可以提交请求。 可以通过两种方法来提交请求：通过[**SdBusSubmitRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest)例程同步，并通过[**SdBusSubmitRequestAsync**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequestasync)例程进行异步处理。 这两个例程均由 SD 总线库（*sdbus*）导出。

同步请求例程使用两个参数：接口上下文和请求数据包。

<a href="" id="interface-context"></a>**接口上下文**  
设备驱动程序在使用[**SdBusOpenInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbusopeninterface)打开 SD 接口后，从[**SDBUS\_接口**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537923(v=vs.85))的**上下文**成员检索接口上下文\_标准结构。 每当驱动程序调用接口中的方法时，该驱动程序都必须传递此上下文信息。

<a href="" id="request-packet"></a>**请求数据包**  
设备驱动程序必须分配和初始化[**SDBUS\_请求\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))结构。 此结构指定请求函数和请求的其他特征。

由于**SdBusSubmitRequest**是同步的，因此不会返回状态\_"挂起"。 设备驱动程序必须以 IRQL 运行 &lt; 在调用此例程时调度\_级别。

异步请求例程使用以下五个参数：接口上下文、请求数据包、IRP、指向完成例程的指针和完成上下文。

<a href="" id="interface-context"></a>**接口上下文**  
此参数与用于同步事例的相同名称的参数相同。

<a href="" id="request-packet"></a>**请求数据包**  
此参数与用于同步事例的相同名称的参数相同。

<a href="" id="irp"></a>**IRP**  
此参数包含设备驱动程序已分配的 IRP，或包含驱动程序从驱动程序堆栈中的驱动程序接收的 IRP。 IRP 用作请求的运营商。

<a href="" id="completion-routine"></a>**完成例程**  
此参数为 IRP 参数中提供的 IRP 保存[**IoCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程。

<a href="" id="user-context"></a>**用户上下文**  
此参数保存一个指向用户上下文数据的指针，系统会将该指针传递到完成例程参数中指定的完成例程。

当设备驱动程序调用**SdBusSubmitRequestAsync**例程时，该设备驱动程序必须在 IRQL &lt;= 调度\_级别运行。 **SdBusSubmitRequest**是分配其自己的 IRP 并调用**SdBusSubmitRequestAsync**的包装器。 提供此方法是为了方便驱动程序编写器。

以下各节提供了一些代码示例，这些代码示例演示了设备驱动程序如何提交 SD 请求的两个主要类别：有关不同请求的说明，请参阅[**SD\_REQUEST\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)。

## <a name="secure-digital-sd-property-requests"></a>安全数字（SD）属性请求


安全数字（SD）卡驱动程序使用属性请求来读取或设置卡属性。 例如，SD 卡驱动程序可能会读取属性，以确定 SD 卡上的写保护交换机是否处于锁定位置，或者多功能 SDIO 卡上某个特定功能的驱动程序是否可以请求将总线驱动程序分配给函数。

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

在此代码示例中，设备驱动程序初始化 SD bus 请求数据包， [**SDBUS\_请求\_数据包**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff537931(v=vs.85))，并将其传递给[**SdBusSubmitRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nf-ntddsd-sdbussubmitrequest)。 完全初始化的请求数据包具有以下特征：

<a href="" id="type-of-the-request"></a>**请求的类型**  
此代码示例指定了一个 SDRF\_获取请求数据包的**RequestFunction**成员中\_属性请求，指示总线驱动程序从卡中检索属性。 有关 SDRF\_获取\_属性请求的说明，请参阅[**SD\_请求\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sd_request_function)。

<a href="" id="property-to-retrieve"></a>**要检索的属性**  
此代码示例在请求数据包的**GetSetProperty**成员中指定了 SDP\_函数\_NUMBER 属性，该属性指示总线驱动程序检索 "函数编号" 属性的内容。 有关 SDP\_函数\_NUMBER 属性的说明，请参阅[**SDBUS\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/ne-ntddsd-sdbus_property)。

<a href="" id="property-contents-and-length"></a>**属性内容和长度**  
此代码示例将指针放置在设备扩展

请求数据包的**GetSetProperty**成员。 总线驱动程序会将函数编号存储在此位置。 示例代码还将此缓冲区的大小存储在请求数据包的**GetSetProperty**成员中。

## <a name="secure-digital-sd-device-command-requests"></a>安全数字（SD）设备命令请求


驱动程序使用安全数字（SD）卡命令请求将命令发送到 SD 设备。 SD 命令的协议是在*安全数字卡*规范中定义的。 当[**IRP\_MN\_START\_设备 IRP 开始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)设备成功完成之后，驱动程序可以在任何时间发送命令请求。

本部分包含两个代码示例：一个命令请求，该请求使用直接 i/o 从 SD 卡的注册读取一个字节的数据，并使用扩展 i/o 将更多的数据写入 SD 卡。 第二部分中的说明取决于第一个部分，因此读者应该在学习第二部分之前研究第一部分：

[使用的安全数字请求](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538051(v=vs.85))

[使用扩展 i/o 的安全数字请求](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff538055(v=vs.85))

 

 




