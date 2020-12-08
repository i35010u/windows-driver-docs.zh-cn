---
title: 筛选光栅数据
description: 筛选光栅数据
keywords:
- Unidrv，光栅数据筛选
- GPD 文件 WDK Unidrv，光栅数据筛选
- 筛选光栅数据 WDK 打印
- 光栅数据筛选 WDK Unidrv
- 后处理扫描行数据流 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 033eef1c5c0c10b94ccafd38608eedf6290a55a8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797085"
---
# <a name="filtering-raster-data"></a>筛选光栅数据





如果要在后台处理扫描行数据流之前提供其自定义的后处理，可以在 [呈现插件](rendering-plug-ins.md)中实现 [**IPrintOemUni：： FilterGraphics**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)方法来执行此操作。 没有与此 Unidrv 功能关联的 GPD 文件项。

有关详细信息，请参阅 [自定义数据流筛选](customized-data-stream-filtering.md)。

 

