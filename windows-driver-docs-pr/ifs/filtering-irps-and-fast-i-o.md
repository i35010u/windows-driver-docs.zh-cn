---
title: 筛选 Irp 和快速 I/O
description: 筛选 Irp 和快速 I/O
ms.assetid: fad124b0-525d-4ff9-8f2c-3817fc76685c
keywords:
- 筛选驱动程序 WDK 文件系统，IRP 筛选
- 文件系统筛选器驱动程序 WDK，IRP 筛选
- Irp WDK 文件系统
- 筛选 Irp WDK 文件系统
- 筛选快速 I/O WDK 文件系统
- 筛选 WDK 文件系统的快速 I/O
- I/O WDK 的文件系统
- 调度例程 WDK 文件系统
- I/O 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84b309bdb20036e4d89a7cd2b6df275bddcd3df3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541939"
---
# <a name="filtering-irps-and-fast-io"></a>筛选 Irp 和快速 I/O


## <span id="ddk_filtering_irps_and_fast_io_if"></span><span id="DDK_FILTERING_IRPS_AND_FAST_IO_IF"></span>


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

文件系统筛选器驱动程序筛选一个或多个文件系统或文件系统卷的 I/O 请求。 每个 I/O 请求显示为 I/O 请求数据包 (IRP) 或快速 I/O 请求。 Irp 是由驱动程序的 IRP 调度例程处理的 I/O 系统结构。 快速 I/O 请求都由驱动程序的快速 I/O 回调例程处理。

初始化筛选器驱动程序时，其**DriverEntry**例程注册筛选器驱动程序的 IRP 调度例程和快速 I/O 回调例程。 只有一组这些例程可针对每个筛选器驱动程序注册。

某些类型的 Irp 具有快速 I/O 等效项，以及一些快速 I/O 请求具有 IRP 等效项。 但是，Irp 处理多种类型的不能快速 I/O 的 I/O。 此外，某些专用的快速 I/O 例程用于 preacquire 缓存管理器或内存管理器的文件系统资源，而无需创建 IRP。 因此，大多数情况下，Irp 和快速 I/O 请求执行单独的角色在 I/O 操作中。

本部分介绍以下主题：

[Irp 是不同于快速 I/O](irps-are-different-from-fast-i-o.md)

[类型的文件系统筛选器驱动程序设备对象](types-of-device-objects-used-by-file-system-filter-drivers.md)

 

 




