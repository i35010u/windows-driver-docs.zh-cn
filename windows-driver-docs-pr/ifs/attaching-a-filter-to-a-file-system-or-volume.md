---
title: 将筛选器附加到文件系统或卷
description: 将筛选器附加到文件系统或卷
ms.assetid: 7c5059b3-cd9f-4a83-8f78-5a2fcc96b246
keywords:
- 筛选器驱动程序 WDK 文件系统，将附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 附加到文件系统卷的筛选器
- WDK 卷文件系统，将附加筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b0cda49c9fe05a38cec7c293511212eee6558b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375731"
---
# <a name="attaching-a-filter-to-a-file-system-or-volume"></a>将筛选器附加到文件系统或卷


## <span id="ddk_attaching_a_filter_to_a_file_system_or_volume_if"></span><span id="DDK_ATTACHING_A_FILTER_TO_A_FILE_SYSTEM_OR_VOLUME_IF"></span>


文件系统筛选器驱动程序将其自身附加到一个或多个已装载的卷和筛选器在其上的所有 I/O 操作。 但是，它是如何确定要将自身附加到的卷？ Windows Driver Kit (WDK) 中的示例筛选器驱动程序演示了两个最常见的方法，这在其中完成：

-   最终用户可以指定的卷进行筛选，例如，键入卷的驱动器号。 最终用户的命令中继到筛选器驱动程序，因为私有[ **IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)请求。

-   文件系统筛选器驱动程序可以将附加到一个或多个文件系统驱动程序，侦听[ **IRP\_MJ\_文件\_系统\_控制**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)，IRP\_MN\_装载\_批量请求，并将附加到卷，因为它们已装载。

**请注意**  通常应采用的驱动器号的卷映射是一个对多，不一对一。 这是因为高级的存储功能，如动态卷和卷装入点。

 

**请注意**  不应假定该 IRP\_MN\_装载\_批量请求始终以同步方式处理文件系统。 例如，软盘驱动器都可被装入以异步方式是否有没有软盘驱动器中。 因此筛选器驱动程序应准备好传播**PendingReturned**其装入完成例程中的标志。 有关详细信息，请参阅"[检查 PendingReturned 标志](checking-the-pendingreturned-flag.md)。"

 

文件系统筛选器驱动程序可以将附加到，并筛选的任何文件系统卷的 I/O。 它们不能直接连接到存储设备，如磁盘驱动器或分区。 此外，它们不能将附加到单个目录或文件。

有关详细信息，请参阅下列主题：

[创建筛选器设备对象](creating-the-filter-device-object.md)

[将筛选设备对象附加到目标设备对象](attaching-the-filter-device-object-to-the-target-device-object.md)

[传播 DO\_缓冲\_IO 和 DO\_直接\_IO 标志](propagating-the-do-buffered-io-and-do-direct-io-flags.md)

[传播文件\_设备\_SECURE\_打开标志](propagating-the-file-device-secure-open-flag.md)

[清除 DO\_设备\_正在初始化标志](clearing-the-do-device-initializing-flag.md)

 

 




