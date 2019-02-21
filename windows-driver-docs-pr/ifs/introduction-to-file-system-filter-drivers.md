---
title: 文件系统筛选器驱动程序简介
description: 文件系统筛选器驱动程序简介
ms.assetid: 7947aaa9-57d4-4adf-8214-151a4755939b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8362985cd6818e65fe9504d437ba8a9365a16cae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519321"
---
# <a name="introduction-to-file-system-filter-drivers"></a>文件系统筛选器驱动程序简介


## <span id="ddk_introduction_to_file_system_filter_drivers_if"></span><span id="DDK_INTRODUCTION_TO_FILE_SYSTEM_FILTER_DRIVERS_IF"></span>


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

本部分介绍文件系统筛选器驱动程序。 它包括以下主题：

[什么是文件系统筛选器驱动程序？](what-is-a-file-system-filter-driver-.md)

[文件系统筛选器驱动程序不是设备驱动程序](file-system-filter-drivers-are-not-device-drivers.md)

[安装文件系统筛选器驱动程序](installing-a-file-system-filter-driver.md)

[初始化文件系统筛选器驱动程序](initializing-a-file-system-filter-driver.md)

[将筛选器附加到文件系统或卷](attaching-a-filter-to-a-file-system-or-volume.md)

 

 




