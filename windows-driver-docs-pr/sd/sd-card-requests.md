---
title: SD 卡请求
description: SD 卡请求
ms.assetid: 3c04573a-5fe7-4332-b899-5aff3234f1ad
keywords:
- SD WDK 总线请求处理
- I/O WDK SD 总线
- 请求处理 WDK SD 总线
- 同步请求 WDK SD 总线
- 异步请求 WDK SD 总线
- SdBusSubmitRequest
- SdBusSubmitRequestAsync
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2541b8022101770a40fb103dfaff561f49fd41a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519104"
---
# <a name="sd-card-requests"></a>SD 卡请求


Secure Digital (SD) 卡设备驱动程序已打开并初始化 SD 总线驱动程序的接口后，它可以提交请求。 有两种方法用于将请求提交： 同步的方式[ **SdBusSubmitRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff537909)例程，并以异步方式通过的方式[ **SdBusSubmitRequestAsync** ](https://msdn.microsoft.com/library/windows/hardware/ff537914)例程。 这两个这些例程都由 SD 总线库导出 (*sdbus.lib*)。

同步请求例程采用两个参数： 接口上下文和请求数据包。

<a href="" id="interface-context"></a>**接口上下文**  
设备驱动程序会检索来自接口上下文**上下文**的成员[ **SDBUS\_接口\_标准**](https://msdn.microsoft.com/library/windows/hardware/ff537923)后结构打开的 SD 接口[ **SdBusOpenInterface**](https://msdn.microsoft.com/library/windows/hardware/ff537906)。 该驱动程序必须通过此上下文信息在每当它调用的方法在界面中。

<a href="" id="request-packet"></a>**请求数据包**  
设备驱动程序必须分配并初始化[ **SDBUS\_请求\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff537931)结构。 此结构指定请求函数和请求的其他特征。

因为**SdBusSubmitRequest**是同步的它不返回状态\_PENDING。 设备驱动程序必须运行在 IRQL&lt;调度\_级别时它将调用此例程。

异步请求例程采用以下五个参数： 接口上下文、 请求数据包，IRP，指向完成例程，并完成上下文的指针。

<a href="" id="interface-context"></a>**接口上下文**  
此参数是与参数相同的同步的情况下使用的相同名称。

<a href="" id="request-packet"></a>**请求数据包**  
此参数是与参数相同的同步的情况下使用的相同名称。

<a href="" id="irp"></a>**IRP**  
此参数包含 IRP 的已分配的设备驱动程序或从驱动程序收到的驱动程序驱动程序堆栈中位于其上方的 IRP。 IRP 用作请求承运人。

<a href="" id="completion-routine"></a>**完成例程**  
此参数包含[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354) IRP IRP 参数中提供的例程。

<a href="" id="user-context"></a>**用户上下文**  
此参数保留一个指向系统将传递给完成例程完成例程参数中指定的用户上下文数据。

设备驱动程序必须运行在 IRQL &lt;= 调度\_级别时，它调用**SdBusSubmitRequestAsync**例程。 **SdBusSubmitRequest**是分配其自己的 IRP 和调用的包装**SdBusSubmitRequestAsync**。 它提供为方便起见，驱动程序编写器。

以下部分提供了代码示例，展示了如何将设备驱动程序将提交每个 SD 的请求的两个主要类别：有关说明不同的请求，请参阅[ **SD\_请求\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff538012)。

## <a name="secure-digital-sd-property-requests"></a>安全数字 (SD) 属性的请求


安全数字 (SD) 卡驱动程序使用属性的请求读取或设置卡属性。 例如，SD 卡驱动程序可能会读取属性以确定是否在 SD 卡上的写保护开关处于锁定位置，或多功能 SDIO 卡上的特定函数的驱动程序可能会请求总线驱动程序分配到的编号它所管理的函数。

下面的代码示例演示了如何多功能卡上的函数的驱动程序可能从总线驱动程序请求其函数号：

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

在此代码示例中，设备驱动程序初始化 SD 总线请求数据包[ **SDBUS\_请求\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff537931)，并将其传递给[ **SdBusSubmitRequest**](https://msdn.microsoft.com/library/windows/hardware/ff537909)。 完全初始化的请求包具有以下特征：

<a href="" id="type-of-the-request"></a>**请求的类型**  
代码示例指定 SDRF\_获取\_中的属性请求**RequestFunction**请求数据包，这会指示总线驱动程序从卡中检索属性的成员。 有关说明 SDRF\_获取\_属性请求，请参阅[ **SD\_请求\_函数**](https://msdn.microsoft.com/library/windows/hardware/ff538012)。

<a href="" id="property-to-retrieve"></a>**若要检索的属性**  
代码示例指定 SDP\_函数\_中的 NUMBER 属性**Parameters.GetSetProperty.Property**请求数据包，这会指示要检索的内容的总线驱动程序的成员函数编号属性。 有关说明 SDP\_函数\_NUMBER 属性，请参阅[ **SDBUS\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff537927)。

<a href="" id="property-contents-and-length"></a>**属性内容和长度**  
代码示例将指针放到缓冲区中的设备扩展中

**Parameters.GetSetProperty.Buffer**请求数据包的成员。 总线驱动程序将在此位置中存储的函数号。 示例代码还将存储在此缓冲区的大小**Parameters.GetSetProperty.Length**请求数据包的成员。

## <a name="secure-digital-sd-device-command-requests"></a>安全数字 (SD) 设备命令请求


驱动程序使用 Secure Digital (SD) 卡命令请求将命令发送到 SD 设备。 在中定义的协议为 SD 命令*安全数字卡*规范。 驱动程序可以在任何时间之后发送命令请求[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)使设备开始的 IRP 成功完成。

本部分包含两个代码示例： 从 SD 卡使用直接 I/O 的寄存器中读取一个字节的数据的命令请求并将较大数量的数据写入到 SD 卡使用扩展的 I/O 的设备命令请求。 第二个部分中的说明取决于在第一天，因此，读取器应之前的学习第一部分学习第二个：

[安全数字请求使用的](https://msdn.microsoft.com/library/windows/hardware/ff538051)

[安全数字请求使用的扩展 I/O](https://msdn.microsoft.com/library/windows/hardware/ff538055)

 

 




