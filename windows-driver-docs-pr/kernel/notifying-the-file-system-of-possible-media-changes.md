---
title: 向文件系统通知可能发生了媒体更改
description: 向文件系统通知可能发生了媒体更改
ms.assetid: b1956370-ec9c-4a43-90a8-12705d28e314
keywords:
- 可移动媒体 WDK 内核，通知媒体更改
- 通知 WDK 可移动介质
- 媒体更改通知 WDK 可移动媒体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bbf701203cd0be385a1937e52f3edc293826f0f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191328"
---
# <a name="notifying-the-file-system-of-possible-media-changes"></a>向文件系统通知可能发生了媒体更改





可移动媒体设备驱动程序必须确保 **DeviceObject** (输入所表示的设备的媒体未更改为每个发送 irp) 的驱动程序例程，只要驱动程序处理的 irp 请求传输到媒体或设备 i/o 控制操作（这些操作影响媒体）。 检查已更改的媒体的最佳可能时间是，如果物理设备始终向驱动程序通知有关这些状态更改的信息，则从无媒体状态转换到媒体显示状态。

如果其物理设备指示在驱动程序开始 i/o 操作之前或在操作过程中媒体的状态可能已更改，则驱动程序必须执行以下操作：

1.  通过检查 VPB 中的 VPB 装入标志，确保卷已装入 \_ 。 *VPB*  (如果未装入卷，则驱动程序不得设置 " \_ 验证 \_ 卷位"。 驱动程序应将 **IoStatus** 设置为状态 \_ IO \_ 设备 \_ 错误，将 **IoStatus** 设置为零，并通过 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。 ) 

2.  将**DeviceObject** By or**标志**中的**标志**设置为 DO \_ VERIFY \_ VOLUME。

3.  将 IRP 中的 **IoStatus** 块设置为以下内容：
    -   **状态**设置为 " \_ 需要验证" \_
    -   **信息** 设置为零

4.  在使用**IoStatus**块完成任何 IRP，其中**status**字段未设置为 "成功" 状态时 \_ ，驱动程序必须调用[**IoIsErrorUserInduced**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiserroruserinduced)，这将为以下任何**状态值**返回布尔值**TRUE** ：

    -   状态 \_ 验证是否 \_ 必需
    -   状态 \_ 不 \_ 是 \_ 设备中的媒体 \_
    -   状态 \_ 错误 \_ 卷
    -   状态 \_ 无法识别的 \_ 媒体
    -   状态 \_ 媒体 \_ 写入 \_ 受保护
    -   状态 \_ IO \_ 超时
    -   状态 \_ 设备 \_ 未 \_ 就绪

    如果 **IoIsErrorUserInduced** 返回 **TRUE**，则驱动程序必须调用 [**IoSetHardErrorOrVerifyDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice) ，以便 FSD 可以向用户打开一个对话框，然后，用户可以选择提供正确的媒体、重试原始请求或取消请求的操作。

 

