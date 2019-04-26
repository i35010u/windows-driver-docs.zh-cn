---
title: PoolMon 概述
description: PoolMon 概述
ms.assetid: c540e156-f0ce-4ac2-88e3-2e199b513abe
keywords:
- PoolMon WDK，有关 PoolMon
- 内存池监视器 WDK，有关内存池监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87fe77831ccf023913b3e74fc37370f0dc97d6a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327259"
---
# <a name="poolmon-overview"></a>PoolMon 概述


## <span id="ddk_poolmon_overview_tools"></span><span id="DDK_POOLMON_OVERVIEW_TOOLS"></span>


Poolmon 可显示有关内存分配的下列数据。 数据按分配的池标记。

-   分配操作和 free 操作 （和未释放的内存分配） 的数目。

-   分配操作和更新之间的可用操作的数目变化。

-   按标记，以字节为单位使用的内存分配的总大小和平均分配的大小。

-   以字节为单位使用更新之间更改。

-   驱动程序分配的标记值。

PoolMon 还显示常规内存信息，包括总计和可用内存、 页面错误、 内核的物理内存，已提交的内存和提交限制、 峰值内存和分页和非分页池的大小。

使用 PoolMon，还可以：

-   排序和重新配置 PoolMon 显示在运行时。

-   将配置的数据保存到一个文件。

-   生成本地系统 (仅适用于 32 位 Windows) 上的驱动程序使用的标记的文件。

 

 





