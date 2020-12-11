---
title: 使用 NTSTATUS 值
description: 使用 NTSTATUS 值
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
ms.openlocfilehash: 0cef14c66feb8e77dc9ce0b6ec7d8d616535cc13
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091196"
---
# <a name="using-ntstatus-values"></a>使用 NTSTATUS 值





许多内核模式 [标准驱动程序例程](./introduction-to-standard-driver-routines.md) 和驱动程序支持例程对返回值使用 NTSTATUS 类型。 此外，当 [完成 irp](completing-irps.md)时，驱动程序在 Irp 的 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)结构中提供一个 NTSTATUS 类型的值。 在 Ntdef 中定义了 NTSTATUS 类型，系统提供的状态代码是在 Ntstatus 中定义的。  (供应商还可以定义专用状态代码，不过它们很少需要。 有关详细信息，请参阅 [定义新的 NTSTATUS 值](defining-new-ntstatus-values.md)。 ) 

NTSTATUS 值分为四种类型：成功值、信息性值、警告和错误值。

为每个类型分配了多个值。 测试成功从例程进行返回的常见错误是将例程的返回值与状态成功进行比较 \_ 。 此比较仅检查几个成功值中的一个。

测试返回值时，应使用 Ntdef 中定义的以下系统提供的宏之一)  (：

<a href="" id="nt-success-status-"></a>NT \_ SUCCESS (*状态*)   
如果由 *Status* 指定的返回值为成功类型，则计算结果为 **TRUE** () 或 (0x40000000 − 0x7fffffff) 的信息性类型。

<a href="" id="nt-information-status-"></a>NT \_ INFORMATION (*状态*)   
如果由 *Status* 指定的返回值为信息类型，则计算结果为 **TRUE** (0x40000000 − 0x7fffffff) 。

<a href="" id="nt-warning-status-"></a>NT \_ WARNING (*状态*)   
如果由 *Status* 指定的返回值为警告类型 (0X80000000 − 0xBFFFFFFF) ，则计算结果为 **TRUE** 。

<a href="" id="nt-error-status-"></a>NT \_ 错误 (*状态*)   
如果由 *Status* 指定的返回值为错误类型，则计算结果为 **TRUE** (0xC0000000-0xffffffff) 。

例如，假设驱动程序调用 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) 来注册设备接口。 如果驱动程序使用 NT SUCCESS 宏检查返回值 \_ ，则当例程返回状态 \_ "成功" （指示没有错误）或返回 "信息状态" 状态 \_ 对象 \_ 名称 \_ （表示已注册了设备接口）时，宏的计算结果将为 TRUE。

作为另一个示例，假定驱动程序调用 [**ZwEnumerateKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey) 来枚举指定注册表项的子项。 如果 NT \_ SUCCESS 宏的计算结果为 **FALSE**，则可能是因为例程返回状态 \_ 无效 \_ 参数，这是一个错误代码，或者是因为例程返回了 \_ "状态" \_ \_ ，这是一条警告代码。

作为最后一个示例，假定驱动程序发送 IRP，该 IRP 会导致较低级别的驱动程序从设备读取信息。 如果发出请求的驱动程序指定的缓冲区太小而无法接收任何信息，则低级驱动程序可能会通过返回状态 \_ 缓冲区 \_ 太小来做出响应 \_ ，这是一个错误代码。 如果第一个驱动程序指定的缓冲区可接收某些（但不是全部）请求的信息，则低级驱动程序可能会通过提供尽可能多的数据来做出响应，然后返回状态 \_ 缓冲区 \_ 溢出，这是一条警告代码。 请注意，如果第一个驱动程序在错误情况下使用 NT SUCCESS 测试状态值 \_ \_ ，则可能会无意中删除接收到的某些信息。

 

