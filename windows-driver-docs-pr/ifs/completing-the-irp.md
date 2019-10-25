---
title: 完成 IRP
description: 完成 IRP
ms.assetid: 3174b36c-feb5-497c-a6e4-0d070c658899
keywords:
- IRP 调度例程 WDK 文件系统，完成 Irp
- 完成 i/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7344d1d44aa4300a72dabc15da44ccec319abf6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841467"
---
# <a name="completing-the-irp"></a>完成 IRP


## <span id="ddk_handling_the_control_device_object_case_if"></span><span id="DDK_HANDLING_THE_CONTROL_DEVICE_OBJECT_CASE_IF"></span>


每个调度例程都会在其*DeviceObject*参数中收到指向 IRP 目标设备对象的指针。 如果筛选器驱动程序具有控制设备对象（CDO），则在对 IRP 执行任何处理之前，调度例程应检查*DeviceObject*指针是否指向筛选器驱动程序的 CDO。

文件系统筛选器驱动程序不需要支持特别发送到 CDO 的任何 i/o 操作。 （有关常见支持的操作的详细信息，请参阅[筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)。）但是，CDO 必须完成发送到它的每个 IRP。

若要*完成*IRP，调度例程必须执行以下所有步骤：

1.  将**Irp&gt;IoStatus**设置为相应的 NTSTATUS 值。

2.  调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)将 IRP 返回到 I/o 管理器。

3.  返回与步骤1中的调用方相同的状态值。

完成 IRP 有时被称为 "成功" 或 "失败" IRP：

-   若要*成功*完成 IRP，请使用成功或信息性的 NTSTATUS 值（如状态\_成功）完成此目的。

-   若要使 IRP*失败*，请使用错误或警告 NTSTATUS 值（如状态\_无效\_设备\_请求或状态\_缓冲区\_溢出来完成它。

NTSTATUS 值在 ntstatus 中定义。 这些值分为四类：成功、信息性、警告和错误。 有关详细信息，请参阅[使用 NTSTATUS 值](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-ntstatus-values)。

**请注意**   尽管状态\_挂起是成功的 NTSTATUS 值，但它是一个编程错误，用于完成状态为\_挂起的 IRP。

 

 

 




