---
title: PoolMon 概述
description: PoolMon 概述
keywords:
- PoolMon WDK，关于 PoolMon
- 内存池监视器 WDK，关于内存池监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0000d3714aee96d39280b1274eb1da1d420a3c5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841015"
---
# <a name="poolmon-overview"></a>PoolMon 概述


## <span id="ddk_poolmon_overview_tools"></span><span id="DDK_POOLMON_OVERVIEW_TOOLS"></span>


PoolMon 显示有关内存分配的下列数据。 数据按分配的池标记排序。

-   分配操作数和可用操作 (和 unfreed 内存分配) 。

-   分配操作数和更新之间的自由操作的变化。

-   按标记分配的内存总大小（以字节为单位）和平均分配大小。

-   更新之间使用的字节数的更改。

-   用于分配标记值的驱动程序。

PoolMon 还会显示一般内存信息，其中包括总计和可用内存、页面错误、内核物理内存、已提交的内存和提交限制、峰值内存以及分页池和非分页池的大小。

使用 PoolMon，你还可以：

-   在 PoolMon 显示正在运行时对其进行排序和重新配置。

-   将配置的数据保存到文件。

-   为本地系统上的驱动程序所使用的标记生成一个文件 32 (仅) 的 Windows。

 

 





