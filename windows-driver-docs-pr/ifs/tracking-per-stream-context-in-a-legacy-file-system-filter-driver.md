---
title: 跟踪每个 Stream 上下文中的旧文件系统筛选器驱动程序
description: 跟踪每个 Stream 上下文中的旧文件系统筛选器驱动程序
ms.assetid: d908ee30-a433-460c-8c14-883702b4f810
keywords:
- 跟踪 WDK 文件系统的上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76700da337bb0b7d4b6a95c1cfc69f76f95e83b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526583"
---
# <a name="tracking-per-stream-context-in-a-legacy-file-system-filter-driver"></a>跟踪每个 Stream 上下文中的旧文件系统筛选器驱动程序


## <span id="ddk_tracking_per_stream_context_in_a_file_system_filter_driver_if"></span><span id="DDK_TRACKING_PER_STREAM_CONTEXT_IN_A_FILE_SYSTEM_FILTER_DRIVER_IF"></span>


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

本部分介绍了 Microsoft Windows XP 和更高版本的操作系统版本中跟踪的每个流上下文。 讨论了以下主题：

[文件流、 Stream 上下文和每个 Stream 上下文](file-streams--stream-contexts--and-per-stream-contexts.md)

[创建和使用每个 Stream 上下文结构](creating-and-using-per-stream-context-structures.md)

 

 




