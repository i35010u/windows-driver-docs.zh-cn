---
title: 文件系统筛选器驱动程序
description: 文件系统筛选器驱动程序
ms.assetid: 9ea59c4a-d6be-4081-82e7-46539d0a1dbd
keywords:
- 筛选器驱动程序 WDK 文件系统
- 文件系统筛选器驱动程序 WDK
- 文件系统驱动程序 WDK，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2581ddb31c498e6bb6ffede13838654294c45c36
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566795"
---
# <a name="file-system-filter-drivers"></a>文件系统筛选器驱动程序


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

本部分包括描述文件系统筛选器驱动程序的以下主题：

-   [文件系统基础知识](file-system-fundamentals.md)
-   [文件系统筛选器驱动程序简介](introduction-to-file-system-filter-drivers.md)
-   [筛选 Irp 和快速 I/O](filtering-irps-and-fast-i-o.md)
-   [编写 IRP 调度例程](writing-irp-dispatch-routines.md)
-   [使用 IRP 完成例程](using-irp-completion-routines.md)
-   [跟踪每个 Stream 上下文中的旧文件系统筛选器驱动程序](tracking-per-stream-context-in-a-legacy-file-system-filter-driver.md)
-   [跟踪每个文件中的旧文件系统筛选器驱动程序的上下文](tracking-per-file-context-in-a-legacy-file-system-filter-driver.md)
-   [阻止旧版的文件系统筛选器驱动程序](blocking-file-system-filter-drivers.md)

 

 




