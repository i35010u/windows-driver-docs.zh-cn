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
- 信息值 WDK NTSTATUS 值
- 警告 WDK NTSTATUS 值
- 错误值 WDK NTSTATUS 值
- 状态信息 WDK NTSTATUS 值
- 检查返回值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ea1f813b60532a140e1dfd1001d24b2e35afa5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838346"
---
# <a name="using-ntstatus-values"></a>使用 NTSTATUS 值





许多内核模式[标准驱动程序例程](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)和[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)对返回值使用 NTSTATUS 类型。 此外，在[完成 irp](completing-irps.md)时，驱动程序会在 IRP 的[**IO\_状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构中提供一个 NTSTATUS 类型的值。 在 Ntdef 中定义了 NTSTATUS 类型，系统提供的状态代码是在 Ntstatus 中定义的。 （供应商还可以定义专用状态代码，不过它们很少需要。 有关详细信息，请参阅[定义新的 NTSTATUS 值](defining-new-ntstatus-values.md)。）

NTSTATUS 值分为四种类型：成功值、信息性值、警告和错误值。

为每个类型分配了多个值。 测试成功从例程进行返回的常见错误是将例程的返回值与状态\_SUCCESS 进行比较。 此比较仅检查几个成功值中的一个。

测试返回值时，应使用以下系统提供的宏之一（在 Ntdef 中定义）：

<a href="" id="nt-success-status-"></a>NT\_成功（*状态*）  
如果由*Status*指定的返回值为成功类型（0−0x3FFFFFFF）或信息类型（0x40000000），则计算结果为**TRUE** 。

<a href="" id="nt-information-status-"></a>NT\_信息（*状态*）  
如果由*Status*指定的返回值为信息类型（0x40000000），则计算结果为**TRUE** 。

<a href="" id="nt-warning-status-"></a>NT\_警告（*状态*）  
如果由*Status*指定的返回值为警告类型（0X80000000 −0xBFFFFFFF），则计算结果为**TRUE** 。

<a href="" id="nt-error-status-"></a>NT\_错误（*状态*）  
如果由*Status*指定的返回值为错误类型（0xC0000000），则计算结果为**TRUE** 。

例如，假设驱动程序调用[**IoRegisterDeviceInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface)来注册设备接口。 如果驱动程序使用 NT\_SUCCESS 宏来检查返回值，则该宏的计算结果将为**TRUE** ，如果该例程返回状态\_SUCCESS，指示没有错误或返回信息状态状态\_对象\_NAME\_EXISTS，这表示设备接口已注册。

作为另一个示例，假定驱动程序调用[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)来枚举指定注册表项的子项。 如果 NT\_SUCCESS 宏的计算结果为**FALSE**，则可能是因为例程返回状态\_无效的\_参数，这是一个错误代码，或者是因为例程返回了状态\_无\_更多\_项，它是警告代码。

作为最后一个示例，假定驱动程序发送 IRP，该 IRP 会导致较低级别的驱动程序从设备读取信息。 如果发出请求的驱动程序指定的缓冲区太小而无法接收任何信息，则较低级别的驱动程序可能会通过返回\_缓冲区\_\_太小，这是一个错误代码来做出响应。 如果第一个驱动程序指定的缓冲区可接收某些（但不是全部）请求的信息，较低级别的驱动程序可能会通过提供尽可能多的数据来做出响应，然后返回状态\_缓冲区\_溢出，这是一条警告代码。 请注意，如果第一个驱动程序使用 NT\_成功或 NT\_错误来测试状态值，则可能会无意中删除收到的某些信息。

 

 




