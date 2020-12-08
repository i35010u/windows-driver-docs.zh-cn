---
title: 完成 IRP
description: 完成 IRP
keywords:
- IRP 调度例程 WDK 文件系统，完成 Irp
- 完成 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e3449e003b3067d0b98854aa97f8aceea92772a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786843"
---
# <a name="completing-the-irp"></a>完成 IRP


## <span id="ddk_handling_the_control_device_object_case_if"></span><span id="DDK_HANDLING_THE_CONTROL_DEVICE_OBJECT_CASE_IF"></span>


每个调度例程都会在其 *DeviceObject* 参数中收到指向 IRP 目标设备对象的指针。 如果筛选器驱动程序具有 (CDO) 的控制设备对象，则在对 IRP 执行任何处理之前，调度例程应检查 *DeviceObject* 指针是否指向筛选器驱动程序的 CDO。

文件系统筛选器驱动程序不需要支持特别发送到 CDO 的任何 i/o 操作。  (有关常见支持的操作的详细信息，请参阅 [筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)。 ) 不过，CDO 必须完成发送到它的每个 IRP。

若要 *完成* IRP，调度例程必须执行以下所有步骤：

1.  将 **Irp- &gt; IoStatus** 设置为相应的 NTSTATUS 值。

2.  调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 将 IRP 返回到 I/o 管理器。

3.  返回与步骤1中的调用方相同的状态值。

完成 IRP 有时被称为 "成功" 或 "失败" IRP：

-   若要 *成功* 完成 IRP，请使用成功或信息性的 NTSTATUS 值（如状态 \_ 成功）完成。

-   若要使 IRP *失败* ，请使用错误或警告 NTSTATUS 值（如状态： \_ \_ 设备请求无效 \_ 或状态 \_ 缓冲区 \_ 溢出）完成它。

NTSTATUS 值在 ntstatus 中定义。 这些值分为四类：成功、信息性、警告和错误。 有关详细信息，请参阅 [使用 NTSTATUS 值](../kernel/using-ntstatus-values.md)。

**注意**   尽管状态 \_ "挂起" 是成功的 NTSTATUS 值，但它是用于完成状态为 "挂起" 的 IRP 的编程错误 \_ 。

 

 

