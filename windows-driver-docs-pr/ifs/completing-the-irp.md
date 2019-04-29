---
title: 完成 IRP
description: 完成 IRP
ms.assetid: 3174b36c-feb5-497c-a6e4-0d070c658899
keywords:
- IRP 调度例程 WDK 文件系统，完成 Irp
- 完成 I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9bfa4598522deba749cbc0e19761eab473c29d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391119"
---
# <a name="completing-the-irp"></a>完成 IRP


## <span id="ddk_handling_the_control_device_object_case_if"></span><span id="DDK_HANDLING_THE_CONTROL_DEVICE_OBJECT_CASE_IF"></span>


每个调度例程接收指向 IRP 的目标设备对象中其*DeviceObject*参数。 如果筛选器驱动程序具有一个控制设备对象 (CDO)，应检查调度例程是否*DeviceObject* IRP 上执行任何处理之前指针指向筛选器驱动程序的 CDO。

文件系统筛选器驱动程序不需要支持特定于 CDO 发送任何 I/O 操作。 (有关通常支持的操作的详细信息，请参阅[筛选器驱动程序的控制设备对象](the-filter-driver-s-control-device-object.md)。)但是，CDO 必须完成发送给它的每个 IRP。

向*完整*IRP，调度例程必须执行所有以下步骤：

1.  设置**Irp-&gt;IoStatus.Status**为适当的 NTSTATUS 值。

2.  调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)返回 IRP 到 I/O 管理器。

3.  如步骤 1 中所示将同一状态值返回给调用方。

完成 IRP 有时称为"成功"或"失败"IRP:

-   向*成功*IRP 意味着完成与成功或类似于状态的信息性 NTSTATUS 值\_成功。

-   向*失败*IRP 意味着若要完成使用错误或警告 NTSTATUS 值类似于状态\_无效\_设备\_请求或状态\_缓冲区\_溢出。

NTSTATUS 值 ntstatus.h 中发现了定义。 这些值划分为四个类别： 成功后，信息性消息、 警告和错误。 有关详细信息，请参阅[使用 NTSTATUS 值](https://msdn.microsoft.com/library/windows/hardware/ff565436)。

**请注意**  虽然状态\_PENDING 是成功 NTSTATUS 值，而是编程错误才能完成，状态 IRP\_PENDING。

 

 

 




