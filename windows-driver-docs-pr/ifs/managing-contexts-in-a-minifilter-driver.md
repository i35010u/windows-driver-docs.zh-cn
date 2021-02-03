---
title: 关于微筛选器上下文
description: 定义微筛选器上下文和列表类型的微筛选器上下文
keywords:
- 文件系统微筛选器驱动程序 WDK，上下文
- 微筛选器驱动程序 WDK，上下文
- 上下文 WDK 文件系统微筛选器
- 上下文 WDK 文件系统微筛选器，关于上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79d68589ddda3050cb96c6f1c3a7c390624b97eb
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502036"
---
# <a name="about-minifilter-contexts"></a>关于微筛选器上下文

*上下文* 是由微筛选器驱动程序定义的结构，可与筛选器管理器对象关联。
筛选器管理器提供支持，使微筛选器驱动程序可以将上下文与对象关联起来，以跨 i/o 操作保留状态。

## <a name="types-of-contexts"></a>上下文类型

Minifilters 可以为以下对象创建并设置上下文：

- 文件 (Windows Vista 及更高版本) 
- 实例数
- 流
- 流处理 (文件对象) 
-  (Windows Vista 和更高版本的事务) 
- 卷

卷上下文必须从非分页池分配。 所有其他上下文类型都可以从分页或非分页池分配。

## <a name="filter-driver-context-sample-code"></a>筛选器驱动程序上下文示例代码

有关使用上下文的微筛选器驱动程序的示例，请参阅 [CTX 示例](https://github.com/microsoft/Windows-driver-samples/tree/master/filesys/miniFilter/ctx) 。

## <a name="how-to-manage-contexts"></a>如何管理上下文

以下部分介绍如何管理筛选器上下文：

- [注册上下文类型](registering-context-types.md)
- [正在创建上下文](creating-contexts.md)
- [设置上下文](setting-contexts.md)
- [正在获取上下文](getting-contexts.md)
- [引用上下文](referencing-contexts.md)
- [释放上下文](releasing-contexts.md)
- [正在删除上下文](deleting-contexts.md)
- [释放上下文](freeing-contexts.md)
- [上下文的文件系统支持](file-system-support-for-contexts.md)
- [最佳实践](best-practices.md)

有关筛选器管理器提供的支持的信息，请参阅 [支持微筛选器上下文](managing-contexts.md)。
