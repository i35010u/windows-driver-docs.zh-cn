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
ms.openlocfilehash: 6531c7973498d440afac39ba5971a496c04ee14e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827817"
---
# <a name="notifying-the-file-system-of-possible-media-changes"></a>向文件系统通知可能发生了媒体更改





可移动媒体设备驱动程序必须确保每当驱动程序处理请求传入/传出媒体的 IRP 时， **DeviceObject**代表的设备（输入到发送 IRP 的每个驱动程序例程）都不会更改介质影响媒体的设备 i/o 控制操作。 检查已更改的媒体的最佳可能时间是，如果物理设备始终向驱动程序通知有关这些状态更改的信息，则从无媒体状态转换到媒体显示状态。

如果其物理设备指示在驱动程序开始 i/o 操作之前或在操作过程中媒体的状态可能已更改，则驱动程序必须执行以下操作：

1.  通过检查*VPB*中的 VPB\_装载标志来确保卷已装入。 （如果未装入卷，则驱动程序不得设置 DO\_验证\_卷位。 驱动程序应将**IoStatus**设置为状态\_IO\_设备\_错误，将**IoStatus**设置为零，并通过 IRP 调用[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。）

2.  将**DeviceObject** By or**标志**中的**标志**设置为 DO\_验证\_卷。

3.  将 IRP 中的**IoStatus**块设置为以下内容：
    -   **状态**设置为状态\_验证是否需要\_
    -   **信息**设置为零

4.  在使用**IoStatus**块完成任何 IRP 之前，如果 "**状态**" 字段未设置为 "状态"\_成功，则驱动程序必须调用[**IoIsErrorUserInduced**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioiserroruserinduced)，这将为以下任何状态返回布尔值**TRUE**值：

    -   状态\_验证\_必需
    -   \_设备中没有\_媒体\_的状态\_
    -   状态\_错误\_卷
    -   状态\_无法识别的\_媒体
    -   状态\_媒体\_写入\_受保护
    -   状态\_IO\_超时
    -   状态\_设备\_未\_就绪

    如果**IoIsErrorUserInduced**返回**TRUE**，则驱动程序必须调用[**IoSetHardErrorOrVerifyDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iosetharderrororverifydevice) ，以便 FSD 可以为用户打开一个对话框，然后，用户可以选择提供正确的媒体、重试原始请求或取消请求的运作.

 

 




