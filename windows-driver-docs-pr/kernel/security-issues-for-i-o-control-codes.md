---
title: I/O 控制代码的安全问题
description: I/O 控制代码的安全问题
ms.assetid: cab8aed2-7185-4622-9a8f-bc8eab3c8c59
keywords:
- I/O 控制代码 WDK 内核安全性
- 控制代码 WDK Ioctl，安全性
- Ioctl WDK 内核安全性
- 安全 WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8955025721edc1cd7d545c207fa468b638920bc7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563986"
---
# <a name="security-issues-for-io-control-codes"></a>I/O 控制代码的安全问题





安全处理 Irp 包含 I/O 控制代码取决于定义正确 IOCTL 代码以及仔细检查驱动程序将会收到包含 IRP 的参数。

在定义新 IOCTL 代码时，使用以下规则：

-   始终指定*FunctionCode*值等于或大于 0x800。

-   始终指定*RequiredAccess*值。 I/O 管理器不发送 Ioctl，如果调用方没有足够的访问权限。

-   未定义 IOCTL 代码，允许调用方读取或写入的内核内存的非特定区域。

在处理 IOCTL 驱动程序内的代码时，使用以下规则：

-   每当驱动程序的调度例程测试接收的 IOCTL 代码，它们必须始终测试整个 32 位值。

-   驱动程序可以使用[ **IoValidateDeviceIoControlAccess** ](https://msdn.microsoft.com/library/windows/hardware/ff550418)动态执行更严格的访问比指定的检查*RequiredAccess*中的值I/O 控制代码定义。

-   永远不会读取或写入数据多于所指向的缓冲区**Irp-&gt;AssociatedIrp.SystemBuffer**可以包含。 因此，始终检查**Parameters.DeviceIoControl.InputBufferLength**或**Parameters.DeviceIoControl.OutputBufferLength**中[ **IO\_堆栈\_位置**](https://msdn.microsoft.com/library/windows/hardware/ff550659)结构，以确定缓冲区限制。

-   始终为零将包含数据适用于源自 IOCTL 请求的应用程序的驱动程序分配的缓冲区。 这样一来，您将不会意外地敏感将数据复制到应用程序。

-   为方法\_IN\_DIRECT 和方法\_出\_直接传输，请按照上述规则。 此外，检查**NULL**返回值从[ **MmGetSystemAddressForMdlSafe**](https://msdn.microsoft.com/library/windows/hardware/ff554559)，指示映射失败或在提供了长度为零的缓冲区。

-   为方法\_都不传输，请按照中提供的规则[使用既不缓冲 Nor 直接 I/O](using-neither-buffered-nor-direct-i-o.md)。

 

 




