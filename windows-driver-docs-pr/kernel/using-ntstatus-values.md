---
title: 使用 NTSTATUS 值
description: 使用 NTSTATUS 值
ms.assetid: fe823930-e3ff-4c95-a640-bb6470c95d1d
keywords:
- NTSTATUS 值 WDK 内核
- 驱动程序支持例程 WDK 内核
- 返回值 WDK 内核
- 测试返回值 WDK NTSTATUS 值
- 成功值 WDK NTSTATUS 值
- 信息性值 WDK NTSTATUS 值
- 警告 WDK NTSTATUS 值
- 错误值 WDK NTSTATUS 值
- 状态信息 WDK NTSTATUS 值
- 检查返回值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 142d339de566f35ae517d30f16a8c3c5b56fe49d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381603"
---
# <a name="using-ntstatus-values"></a>使用 NTSTATUS 值





很多的内核模式[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)并[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)的 NTSTATUS 类型，用于返回值。 此外，驱动程序提供 NTSTATUS 类型的值在 IRP [ **IO\_状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_status_block)结构时[完成 Irp](completing-irps.md)。 NTSTATUS 类型定义中 Ntdef.h，并在 Ntstatus.h 中定义了系统提供的状态代码。 （供应商还可以定义私有状态代码，尽管在很少需要。 有关详细信息，请参阅[定义新 NTSTATUS 值](defining-new-ntstatus-values.md)。)

NTSTATUS 值划分为四种类型： 成功的值、 信息性值、 警告和错误值。

许多值分配给每个类型。 常见错误，测试从一个例程成功返回时是比较例程的返回值和状态\_成功。 此比较将检查多个成功值之一。

测试返回值时应使用其中一个以下系统提供宏 （Ntdef.h 中定义）：

<a href="" id="nt-success-status-"></a>NT\_SUCCESS(*Status*)  
计算结果为 **，则返回 TRUE**如果返回的值指定*状态*成功类型 （0 − 0x3FFFFFFF） 或信息性的类型 （0x40000000 − 0x7FFFFFFF）。

<a href="" id="nt-information-status-"></a>NT\_INFORMATION(*Status*)  
计算结果为 **，则返回 TRUE**如果返回的值指定*状态*是信息类型 （0x40000000 − 0x7FFFFFFF）。

<a href="" id="nt-warning-status-"></a>NT\_警告 (*状态*)  
计算结果为 **，则返回 TRUE**如果返回的值指定*状态*是警告类型 （0x80000000 − 0xBFFFFFFF）。

<a href="" id="nt-error-status-"></a>NT\_ERROR(*Status*)  
计算结果为 **，则返回 TRUE**如果返回的值指定*状态*是错误类型 (0xC0000000-0xFFFFFFFF)。

例如，假设一个驱动程序调用[ **IoRegisterDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioregisterdeviceinterface)注册设备接口。 如果该驱动程序会检查返回值使用 NT\_成功宏，宏的计算结果为**TRUE**如果例程将返回状态\_成功后，指示没有错误，或如果它返回信息性状态 STATUS\_对象\_名称\_EXISTS，指示已注册的设备接口。

另举一例，假设一个驱动程序调用[ **ZwEnumerateKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwenumeratekey)枚举指定的注册表项的子项。 如果 NT\_成功宏计算结果为**FALSE**，则可能是因为该例程返回状态\_无效\_参数，它是一个错误代码，或因为该例程返回状态\_否\_详细\_条目，这是警告代码。

作为最后一个示例，假设某个驱动程序发送 IRP 导致较低级别驱动程序从设备中读取信息。 如果请求驱动程序指定的缓冲区太小，无法接收任何信息，通过返回状态可能会响应较低级驱动程序\_缓冲区\_过\_小，这是一个错误代码。 如果第一个驱动程序指定的缓冲区，可接收一些，但不是全部的所需的信息，较低级别驱动程序可能会响应提供尽可能多的数据并返回状态\_缓冲区\_溢出，这是警告代码。 请注意，如果第一个驱动程序测试使用 NT 的状态值\_成功或 NT\_错误不正确，它可能会无意中删除一些接收到的信息。

 

 




