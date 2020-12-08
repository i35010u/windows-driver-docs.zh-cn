---
title: 定义新的 NTSTATUS 值
description: 定义新的 NTSTATUS 值
keywords:
- NTSTATUS 值 WDK 内核
- 自定义 NTSTATUS 值 WDK 内核
- IO_ERR_XXX 值
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7e40b5078f2c2446f4ba1f98a8710154ad5fbfa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798127"
---
# <a name="defining-new-ntstatus-values"></a>定义新的 NTSTATUS 值





驱动程序可以将自定义 IO \_ ERR \_ *XXX* 常量定义为记录错误时使用的 **ErrorCode** 值。 同时编写的驱动程序对还可以 \_ 为 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md)请求定义自定义状态 *XXX* 值。

下图显示了32位 NTSTATUS 值中的位域。

![说明 ntstatus 值中的位域的关系图](images/16ntstat.png)

上图中显示的 " **严重性** " 字段指明了严重性代码，该代码必须是以下系统定义的值之一：

<a href="" id="status-severity-success"></a>状态 \_ 严重性 \_ 成功  
指示成功的 NTSTATUS 值（如状态 \_ 成功）或值 IO \_ ERR \_ 重试 \_ 在错误日志数据包中成功。

<a href="" id="status-severity-informational"></a>状态 \_ 严重性 \_ 信息  
指示信息性的 NTSTATUS 值，如状态 \_ 串行 \_ 更多 \_ 写入。

<a href="" id="status-severity-warning"></a>状态 \_ 严重性 \_ 警告  
指示警告的 NTSTATUS 值（如状态 \_ 设备 \_ 纸张 \_ 为空）。

<a href="" id="status-severity-error"></a>状态 \_ 严重性 \_ 错误  
指示错误的 NTSTATUS 值，如 \_ \_ **FinalStatus** \_ \_ \_ 错误日志数据包中的 **ERRORCODE** 值的 FinalStatus 值资源不足或 IO ERR 配置错误。

大多数公共 IO \_ ERR \_ *XXX* 常量都属于状态 \_ 严重性 \_ 错误类别。

**设施** 代码指定生成错误的设备。 对于新的 IO \_ ERR \_ *XXX* 值，驱动程序指定了设施的 "设施 \_ IO \_ 错误 \_ 代码" 值。 **Facility** 对于自定义状态 \_ *XXX* 值，**设备** 的不同值的含义是由驱动程序定义的。

**C** 位指定值是由客户定义还是由 Microsoft 定义。 为客户定义的值设置位，并为 Microsoft 定义的值明确。

驱动程序可定义新 \_ 的 IO ERR \_ *XXX* 值，以确定系统事件日志中的自定义错误消息。 有关如何定义 NTSTATUS 值和它们标识的错误消息的说明，请参阅 [定义自定义错误类型](defining-custom-error-types.md)。

一对驱动程序可定义特定于驱动程序的状态 \_ *XXX* 值，以传达有关私下定义的 [**IRP \_ MJ \_ 内部 \_ 设备 \_ 控制**](./irp-mj-internal-device-control.md)请求的信息。

\_如果可以为该 irp 调用现有的更高级别驱动程序的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程，则类驱动程序必须将任何私有状态 *XXX* 值映射到系统定义的 NTSTATUS 值。

对于配对显示和视频微型端口驱动程序，视频端口驱动程序将执行公共状态 \_ *XXX* 值和视频微型端口驱动程序返回的 Win32 定义常量之间的映射。 有关详细信息，请参阅 [Windows 2000 显示器驱动程序模型中的视频微型端口驱动程序](../display/video-miniport-drivers-in-the-windows-2000-display-driver-model.md)。

对于可以在用户模式下接收的 Irp，驱动程序不能使用自定义 NTSTATUS 值，因为只有系统定义的值才能转换为 Win32 错误代码。

 

