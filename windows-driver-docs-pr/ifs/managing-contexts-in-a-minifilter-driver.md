---
title: 管理微筛选器驱动程序中的上下文
description: 管理微筛选器驱动程序中的上下文
keywords:
- 文件系统微筛选器驱动程序 WDK，上下文
- 微筛选器驱动程序 WDK，上下文
- 上下文 WDK 文件系统微筛选器
- 上下文 WDK 文件系统微筛选器，关于上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e54c73153f52af2c7147265c60f16fb93fd9dae6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828757"
---
# <a name="managing-contexts-in-a-minifilter-driver"></a>管理微筛选器驱动程序中的上下文


## <span id="ddk_writing_a_driverentry_routine_for_a_minifilter_driver_if"></span><span id="DDK_WRITING_A_DRIVERENTRY_ROUTINE_FOR_A_MINIFILTER_DRIVER_IF"></span>


*上下文* 是由微筛选器驱动程序定义的结构，可与筛选器管理器对象关联。 微筛选器驱动程序可以为以下对象创建并设置上下文：

-   文件仅 (Windows Vista 和更高版本。 ) 

-   实例数

-   卷

-   流

-   流处理 (文件对象) 

-   仅 (Windows Vista 和更高版本的事务。 ) 

除了必须从非分页池分配的卷上下文，上下文可以从分页或非分页池进行分配。

筛选器管理器会在其附加到的对象被删除、从卷中分离了筛选器驱动程序实例或卸载微筛选器驱动程序时自动删除上下文。

本节包括：

[注册上下文类型](registering-context-types.md)

[正在创建上下文](creating-contexts.md)

[设置上下文](setting-contexts.md)

[正在获取上下文](getting-contexts.md)

[引用上下文](referencing-contexts.md)

[释放上下文](releasing-contexts.md)

[正在删除上下文](deleting-contexts.md)

[释放上下文](freeing-contexts.md)

[上下文的文件系统支持](file-system-support-for-contexts.md)

[最佳实践](best-practices.md)

 

 




