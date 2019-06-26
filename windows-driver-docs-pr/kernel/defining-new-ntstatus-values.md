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
ms.openlocfilehash: 5a5ac52eed79aaa0dc3da86b68bbcc2aa776374d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377103"
---
# <a name="defining-new-ntstatus-values"></a>定义新的 NTSTATUS 值





驱动程序可以定义自定义 IO\_ERR\_*XXX*常量用作**ErrorCode**值时日志记录错误。 对一起编写的驱动程序还可以定义自定义状态\_*XXX*值为[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)请求。

下图显示在 32 位 NTSTATUS 值中的位域。

![说明 ntstatus 值中的位域的关系图](images/16ntstat.png)

**严重性**在上图中所示的字段指示严重性代码，它必须是系统定义的以下值之一：

<a href="" id="status-severity-success"></a>状态\_严重性\_成功  
指示成功的 NTSTATUS 值，如状态\_成功，则值 IO\_ERR\_重试\_在错误日志数据包中成功进行。

<a href="" id="status-severity-informational"></a>状态\_严重性\_信息  
指示信息性的 NTSTATUS 值，如状态\_串行\_详细\_写入。

<a href="" id="status-severity-warning"></a>状态\_严重性\_警告  
指示警告 NTSTATUS 值，如状态\_设备\_纸张\_为空。

<a href="" id="status-severity-error"></a>状态\_严重性\_错误  
指示错误 NTSTATUS 值，如状态\_不足\_资源**FinalStatus**值或 IO\_ERR\_配置\_的错误**ErrorCode**错误日志数据包中的值。

大多数公共 IO\_ERR\_*XXX*常量属于状态\_严重性\_错误类别。

**设施**代码指定生成该错误的设施。 为新 IO\_ERR\_*XXX*值，驱动程序指定设施\_IO\_错误\_代码值**设施**。 自定义状态\_*XXX*值，不同的值的含义**设施**是驱动程序定义。

**C**位指定的值是否客户定义的或 Microsoft 定义。 位将设置为客户定义的值和清除 Microsoft 定义的值。

驱动程序可以定义新 IO\_ERR\_*XXX*用于标识系统事件日志中的自定义错误消息的值。 有关如何定义 NTSTATUS 值和它们标识的错误消息的说明，请参阅[定义自定义错误类型](defining-custom-error-types.md)。

对驱动程序可以定义特定于驱动程序状态\_*XXX*私下通信有关的信息的值定义[ **IRP\_MJ\_内部\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)来自较低的对中的更高版本的驱动程序的请求。

在类驱动程序必须映射任何私有状态\_*XXX*值为系统定义的 NTSTATUS 值在其完成后 IRP，如果现有更高级别的驱动[ *IoCompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)可能会为该 IRP 调用例程。

对于成对的显示和视频的微型端口驱动程序，视频端口驱动程序将执行公共状态之间的映射\_*XXX*值和返回的微型端口驱动程序的 Win32 定义常量。 有关详细信息，请参阅[视频微型端口驱动程序在 Windows 2000 显示器驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/display/video-miniport-drivers-in-the-windows-2000-display-driver-model)。

因为只有的系统定义的值，可以转化为 Win32 错误代码的驱动程序不能使用可以在用户模式下，接收 Irp NTSTATUS 的自定义值。

 

 




