---
title: 将筛选器附加到文件系统或卷
description: 将筛选器附加到文件系统或卷
ms.assetid: 7c5059b3-cd9f-4a83-8f78-5a2fcc96b246
keywords:
- 筛选器驱动程序 WDK 文件系统，附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 将筛选器附加到文件系统或卷
- 卷 WDK 文件系统，附加筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c44cf7c99277bca7f8872cf0ab1960b92a429e9
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066220"
---
# <a name="attaching-a-filter-to-a-file-system-or-volume"></a>将筛选器附加到文件系统或卷


## <span id="ddk_attaching_a_filter_to_a_file_system_or_volume_if"></span><span id="DDK_ATTACHING_A_FILTER_TO_A_FILE_SYSTEM_OR_VOLUME_IF"></span>


文件系统筛选器驱动程序将自身附加到一个或多个已装入的卷，并筛选出其上所有的 i/o 操作。 但如何确定哪些卷要附加到呢？ Windows 驱动程序工具包 (WDK) 中的示例筛选器驱动程序演示了执行此操作的两种最常见方式：

-   最终用户可以指定要按其进行筛选的卷，例如键入卷的驱动器号。 最终用户的命令作为专用 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md) 请求中继到筛选器驱动程序。

-   文件系统筛选器驱动程序可以附加到一个或多个文件系统驱动程序、侦听 [**irp \_ MJ \_ 文件 \_ 系统 \_ 控制**](./irp-mj-file-system-control.md)、irp \_ MN \_ 装入 \_ 卷请求，以及在装入卷时附加到卷。

**注意**   通常情况下，应假定卷到驱动器号之间的映射是一对多的，而不是一对一的。 这是因为高级存储功能，如动态卷和卷装入点。

 

**注意**   不应假设 IRP \_ MN \_ 装入 \_ 卷请求始终由文件系统同步处理。 例如，如果驱动器中没有软盘，可能会以异步方式装载软盘驱动器。 因此，筛选器驱动程序应准备好在其装入完成例程中传播 **PendingReturned** 标志。 有关详细信息，请参阅 "[检查 PendingReturned 标志](checking-the-pendingreturned-flag.md)"。

 

文件系统筛选器驱动程序可以连接到任何文件系统卷，并对其进行筛选。 它们不能直接附加到存储设备，如磁盘驱动器或分区。 而且，它们不能附加到各个目录或文件。

有关详细信息，请参阅下列主题：

[创建筛选器设备对象](creating-the-filter-device-object.md)

[将筛选器设备对象附加到目标设备对象](attaching-the-filter-device-object-to-the-target-device-object.md)

[传播执行 \_ 缓冲 \_ IO 和执行 \_ 直接 \_ IO 标志](propagating-the-do-buffered-io-and-do-direct-io-flags.md)

[传播文件 \_ 设备 \_ 安全 \_ 打开标志](propagating-the-file-device-secure-open-flag.md)

[清除 "执行 \_ 设备 \_ 初始化" 标志](clearing-the-do-device-initializing-flag.md)

 

