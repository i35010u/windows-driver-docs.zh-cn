---
title: I/O 控制代码的安全问题
description: I/O 控制代码的安全问题
ms.assetid: cab8aed2-7185-4622-9a8f-bc8eab3c8c59
keywords:
- I/o 控制代码 WDK 内核，安全性
- 控制代码 WDK IOCTLs，安全性
- IOCTLs WDK 内核，安全性
- 安全 WDK IOCTLs
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a21f6436d86e339e612f70c48aa00642d2df632
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186717"
---
# <a name="security-issues-for-io-control-codes"></a>I/O 控制代码的安全问题





安全处理包含 i/o 控制代码的 Irp，这一点取决于正确地定义 IOCTL 代码，并仔细检查驱动程序通过 IRP 接收的参数。

定义新的 IOCTL 代码时，请使用以下规则：

-   请始终指定等于或大于0x800 的 *FunctionCode* 值。

-   始终指定 *RequiredAccess* 值。 如果调用方没有足够的访问权限，则 i/o 管理器不发送 IOCTLs。

-   不要定义允许调用方读取或写入非特定内核内存区域的 IOCTL 代码。

在处理驱动程序中的 IOCTL 代码时，请使用以下规则：

-   只要驱动程序的调度例程测试收到 IOCTL 代码，就必须始终测试整个32位值。

-   驱动程序可以使用 [**IoValidateDeviceIoControlAccess**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess) 来动态执行更严格的访问检查，而不是由 i/o 控制代码定义中的 *RequiredAccess* 值所指定的。

-   请勿读取或写入比 Irp 所指向的缓冲区更多的数据， ** &gt;AssociatedIrp.SystemBuffer** 可以包含这些数据。 因此，请始终检查[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构中的**DeviceIoControl InputBufferLength**或**DeviceIoControl OutputBufferLength** ，以确定缓冲区限制。

-   始终为零个驱动程序分配的缓冲区，这些缓冲区将包含适用于发出 IOCTL 请求的应用程序的数据。 这样，你将不会意外地将敏感数据复制到应用程序。

-   对于 \_ \_ 直接传输和方法 \_ OUT \_ 直接传输的方法，请遵循上述规则。 此外，请检查[**MmGetSystemAddressForMdlSafe**](./mm-bad-pointer.md)中是否有**NULL**返回值，该值指示映射失败或提供了零长度的缓冲区。

-   对于 \_ "方法均未传输"，请遵循在中提供的规则，而不 [使用缓冲和直接 i/o](using-neither-buffered-nor-direct-i-o.md)。

 

