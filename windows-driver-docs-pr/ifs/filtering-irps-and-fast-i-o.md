---
title: 筛选 IRP 和快速 I/O
description: 筛选 IRP 和快速 I/O
ms.assetid: fad124b0-525d-4ff9-8f2c-3817fc76685c
keywords:
- 筛选器驱动程序 WDK 文件系统，IRP 筛选
- 文件系统筛选器驱动程序 WDK，IRP 筛选
- Irp WDK 文件系统
- 筛选 Irp WDK 文件系统
- 筛选 fast i/o WDK 文件系统
- 快速 i/o 筛选 WDK 文件系统
- I/o WDK 文件系统
- 调度例程 WDK 文件系统
- I/o 请求 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf01d74ffaec6ab6188d74c50d23e45fcc25bb01
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065050"
---
# <a name="filtering-irps-and-fast-io"></a>筛选 IRP 和快速 I/O

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用带有筛选器管理器支持的 [文件系统微筛选器驱动程序](./filter-manager-concepts.md) ，而不是使用旧的文件系统 若要将旧驱动程序移植到微筛选器驱动程序，请参阅 [迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

文件系统筛选器驱动程序对一个或多个文件系统或文件系统卷的 i/o 请求进行筛选。 每个 i/o 请求都显示为 i/o 请求数据包 (IRP) 或快速 i/o 请求。 Irp 是由驱动程序的 IRP 调度例程处理的 i/o 系统结构。 快速 i/o 请求由驱动程序的快速 i/o 回调例程处理。

当初始化筛选器驱动程序时，它的 **DriverEntry** 例程将注册筛选器驱动程序的 IRP 调度例程和快速 i/o 回调例程。 只能为每个筛选器驱动程序注册一组这些例程。

某些类型的 Irp 具有快速 i/o 等效项，某些快速 i/o 请求具有 IRP 等效项。 但是，Irp 处理的 i/o 类型太多，无法实现快速 i/o。 此外，某些专用的快速 i/o 例程用于 preacquire 缓存管理器或内存管理器的文件系统资源，而无需创建 IRP。 因此，在大多数情况下，Irp 和快速 i/o 请求在 i/o 操作中执行单独的角色。

本部分涵盖了以下主题：

[Irp 不同于快速 i/o](irps-are-different-from-fast-i-o.md)

[文件系统筛选器驱动程序设备对象的类型](types-of-device-objects-used-by-file-system-filter-drivers.md)