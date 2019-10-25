---
title: 定义新的 NTSTATUS 值
description: 定义新的 NTSTATUS 值
ms.assetid: 44211ae4-6bfe-4931-b12c-e590c7aacd97
keywords:
- NTSTATUS 值 WDK 内核
- 自定义 NTSTATUS 值 WDK 内核
- IO_ERR_XXX 值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 700726415ca037a4791361bb3bc19db720a61aa8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836968"
---
# <a name="defining-new-ntstatus-values"></a>定义新的 NTSTATUS 值





驱动程序可以将自定义 IO\_ERR\_*XXX*常量定义为记录错误时用作**ErrorCode**值。 同时编写的驱动程序对还可以为[**IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求定义自定义状态\_*XXX*值。

下图显示了32位 NTSTATUS 值中的位域。

![说明 ntstatus 值中的位域的关系图](images/16ntstat.png)

上图中显示的 "**严重性**" 字段指明了严重性代码，该代码必须是以下系统定义的值之一：

<a href="" id="status-severity-success"></a>状态\_严重性\_成功  
指示成功的 NTSTATUS 值，如 STATUS\_SUCCESS，或值 IO\_ERR\_重试\_在错误日志数据包中成功。

<a href="" id="status-severity-informational"></a>状态\_严重性\_信息  
指示信息性的 NTSTATUS 值，例如状态\_串行\_更多\_写入。

<a href="" id="status-severity-warning"></a>状态\_严重性\_警告  
指示警告的 NTSTATUS 值，例如状态\_设备\_纸张\_为空。

<a href="" id="status-severity-error"></a>状态\_严重性\_错误  
指示错误的 NTSTATUS 值，如状态\_\_资源的**FinalStatus**值不足，或者 IO\_ERR\_配置\_错误日志数据包中的**ERRORCODE**值的错误。

大多数公共 IO\_ERR\_*XXX*常量属于状态\_严重性\_错误类别。

**设施**代码指定生成错误的设备。 对于新的 IO\_ERR\_*XXX*值，驱动程序会指定设备\_IO\_错误\_**设备**的代码值。 对于自定义状态\_*XXX*值，**设备**的不同值的含义是由驱动程序定义的。

**C**位指定值是由客户定义还是由 Microsoft 定义。 为客户定义的值设置位，并为 Microsoft 定义的值明确。

驱动程序可定义新的 IO\_ERR\_*XXX*值，以便在系统事件日志中标识自定义错误消息。 有关如何定义 NTSTATUS 值和它们标识的错误消息的说明，请参阅[定义自定义错误类型](defining-custom-error-types.md)。

一对驱动程序可定义特定于驱动程序的状态\_*XXX*值，以传达有关私下定义的[**IRP\_\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)的。

如果可以为该 IRP 调用现有的更高级别驱动程序的[*IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，则类驱动程序必须将任何私有状态\_*XXX*值映射到系统定义的 NTSTATUS 值。

对于配对的显示和视频微型端口驱动程序，视频端口驱动程序会执行公共状态之间的映射\_*XXX*值和视频微型端口驱动程序返回的 Win32 定义常量。 有关详细信息，请参阅[Windows 2000 显示器驱动程序模型中的视频微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/display/video-miniport-drivers-in-the-windows-2000-display-driver-model)。

对于可以在用户模式下接收的 Irp，驱动程序不能使用自定义 NTSTATUS 值，因为只有系统定义的值才能转换为 Win32 错误代码。

 

 




