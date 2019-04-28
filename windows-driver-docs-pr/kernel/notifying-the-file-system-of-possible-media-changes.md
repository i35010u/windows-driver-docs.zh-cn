---
title: 向文件系统通知可能发生了媒体更改
description: 向文件系统通知可能发生了媒体更改
ms.assetid: b1956370-ec9c-4a43-90a8-12705d28e314
keywords:
- 可移动媒体 WDK 内核的媒体的更改通知
- 通知 WDK 可移动媒体
- 媒体更改通知 WDK 可移动媒体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78c0f16444119e460ddab1434f8422769310ca2c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341959"
---
# <a name="notifying-the-file-system-of-possible-media-changes"></a>向文件系统通知可能发生了媒体更改





可移动介质设备驱动程序必须确保媒体不会更改为所表示的设备**DeviceObject** （发送 IRP 每个驱动程序例程的输入） 时，驱动程序处理 IRP，请求传输与媒体文件和设备 I/O 控制操作，可影响媒体。 如果物理设备始终通知有关这些状态更改的驱动程序，检查已更改的媒体的最佳可能时间是之后从无媒体存在状态到媒体存在状态的转换。

如果其物理设备将指示之前驱动程序开始一个 I/O 操作的媒体的状态可能已更改，或者在操作期间，驱动程序必须执行以下操作：

1.  确保通过检查 VPB 装载卷\_中的已装载标志*VPB*。 (如果不装入卷，该驱动程序必须未设置 DO\_验证\_卷位。 该驱动程序应设置**IoStatus.Status**于状态\_IO\_设备\_错误，设置**IoStatus.Information**为零，并调用[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)与 IRP。)

2.  设置**标志**中**DeviceObject**通过实现或运算**标志**使用\_验证\_卷。

3.  设置**IoStatus**中所示 IRP 块：
    -   **状态**将设置为 STATUS\_验证\_必需
    -   **信息**设置为零

4.  之前完成与任何 IRP **IoStatus**在其中阻止**状态**字段未设置为状态\_成功后，该驱动程序必须调用[ **IoIsErrorUserInduced**](https://msdn.microsoft.com/library/windows/hardware/ff549375)，这会返回一个布尔值**TRUE**以下任一**状态**值：

    -   状态\_验证\_必需
    -   状态\_否\_媒体\_IN\_设备
    -   状态\_错误\_卷
    -   状态\_无法识别\_媒体
    -   状态\_媒体\_编写\_受保护
    -   状态\_IO\_超时
    -   状态\_设备\_不\_准备就绪

    如果**IoIsErrorUserInduced**返回**TRUE**，该驱动程序必须调用[ **IoSetHardErrorOrVerifyDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff549707)以便 FSD 可以打开一个对话框到用户，用户可以选择提供正确的介质，然后重试原始请求，或取消请求的操作。

 

 




