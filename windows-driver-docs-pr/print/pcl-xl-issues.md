---
title: PCL XL 问题
description: PCL XL 问题
ms.assetid: 65db50fb-b58f-44f0-aa2a-67c23a448d32
keywords:
- PCL XL 矢量图形 WDK Unidrv，其他注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e9dfaf95c39ed7ede6cf75da6d7f638717712d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547810"
---
# <a name="pcl-xl-issues"></a>PCL XL 问题





-   Windows XP 和更高版本支持上打印的优化功能**高级**打印机属性页的选项卡。 如果**打印优化**被禁用，Unidrv 打印 PCL XL 光栅模式下的数据。

-   \*MirrorRasterPage？不支持在 PCL XL 模式下。

-   PCL XL 不支持 PCL XL 和光栅模式之间切换。

-   GPD \*PCL XL 微型驱动程序不支持 TextHalftoneThreshold 属性名称。 在任何分辨率的文本是 grayscaled PCL XL 模式中。

 

 




