---
title: PCL XL 问题
description: PCL XL 问题
keywords:
- PCL XL 矢量图形 WDK Unidrv，其他注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec3851c2b7975cbe11272680969cb9d016870eb0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807615"
---
# <a name="pcl-xl-issues"></a>PCL XL 问题





-   Windows XP 和更高版本支持打印机属性页的 " **高级** " 选项卡上的 "打印优化" 功能。 如果禁用 **打印优化** ，Unidrv 将在光栅模式下打印 PCL XL 数据。

-   \*MirrorRasterPage?在 PCL XL 模式下不受支持。

-   PCL XL 不支持在 PCL XL 和光栅模式间切换。

-   \*PCL XL 微型驱动程序上不支持 GPD TextHalftoneThreshold 属性名称。 任何分辨率中的文本都是 PCL XL 模式下的 grayscaled。

 

 




