---
title: 管理微筛选器驱动程序中的上下文
description: 管理微筛选器驱动程序中的上下文
ms.assetid: c7186886-f083-45c9-a39d-3f8ce7df35bb
keywords:
- 文件系统微筛选器驱动程序 WDK，上下文
- 微筛选器驱动程序 WDK、 上下文
- 上下文 WDK 文件系统微筛选器
- 上下文 WDK 文件系统微筛选器，有关上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a4381a3cc85bcb1a93c9ec9d80e1f849184fe5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357560"
---
# <a name="managing-contexts-in-a-minifilter-driver"></a>管理微筛选器驱动程序中的上下文


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


一个*上下文*是一种结构由微筛选器驱动程序，这可能与筛选器管理器对象相关联。 微筛选器驱动程序可以创建并设置以下对象的上下文：

-   文件 (Windows Vista 及更高版本。)

-   Instances

-   卷

-   流

-   Stream 句柄 （文件对象）

-   事务 (Windows Vista 及更高版本。)

除了卷上下文，必须从非分页缓冲池分配，可以从分页或非分页池分配的上下文。

附加到的对象中删除时，从卷分离微筛选器驱动程序实例时或在卸载微筛选器驱动程序时，筛选器管理器将自动删除上下文。

本部分包括：

[注册上下文类型](registering-context-types.md)

[创建上下文](creating-contexts.md)

[设置上下文](setting-contexts.md)

[获取上下文](getting-contexts.md)

[引用上下文](referencing-contexts.md)

[释放上下文](releasing-contexts.md)

[正在删除上下文](deleting-contexts.md)

[释放上下文](freeing-contexts.md)

[用于上下文的文件系统支持](file-system-support-for-contexts.md)

[最佳做法](best-practices.md)

 

 




