---
title: 文件系统基础知识
description: 文件系统基础知识
ms.assetid: 29f0d7cb-9574-489c-affd-31ffdce6abdc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6c2641f7ae5e26172fe8ca8816b732c1229b06
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327483"
---
# <a name="file-system-fundamentals"></a>文件系统基础知识


## <span id="ddk_file_system_fundamentals_if"></span><span id="DDK_FILE_SYSTEM_FUNDAMENTALS_IF"></span>


<div class="alert">
<strong>请注意</strong>最佳的可靠性和性能，我们建议使用<a href="filter-manager-and-minifilter-driver-architecture.md" data-raw-source="[file system minifilter drivers](filter-manager-and-minifilter-driver-architecture.md)">文件系统微筛选器驱动程序</a>而不是旧的文件系统筛选器驱动程序。 此外，旧的文件系统筛选器驱动程序不能将附加到直接访问 (DAX) 卷。 有关文件系统微筛选器驱动程序的详细信息，请参阅<a href="advantages-of-the-filter-manager-model.md" data-raw-source="[Advantages of the Filter Manager Model](advantages-of-the-filter-manager-model.md)">筛选器管理器模型的优势</a>。 若要移植到微筛选器驱动程序的传统的驱动程序，请参阅<a href="guidelines-for-porting-legacy-filter-drivers.md" data-raw-source="[Guidelines for Porting Legacy Filter Drivers](guidelines-for-porting-legacy-filter-drivers.md)">移植旧筛选器驱动程序的指导原则</a>。
</div>
 

本部分介绍基本的文件系统驱动程序概念的文件系统筛选器驱动程序的开发人员很重要。 论述了以下主题：

[加载驱动程序时由什么决定](what-determines-when-a-driver-is-loaded.md)

[文件系统在系统启动期间会发生什么情况](what-happens-to-file-systems-during-system-boot.md)

[存储卷、 存储设备堆栈和文件系统堆栈](storage-device-stacks--storage-volumes--and-file-system-stacks.md)

[装载卷](mounting-a-volume.md)

 

 




