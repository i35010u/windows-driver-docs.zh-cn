---
title: 筛选光栅数据
description: 筛选光栅数据
ms.assetid: 179a2dc0-8794-4934-99b9-eb3f7900536c
keywords:
- Unidrv，光栅数据筛选
- GPD 文件 WDK Unidrv，光栅数据筛选
- 筛选光栅数据 WDK 打印
- 光栅数据筛选 WDK Unidrv
- 后处理扫描行数据流 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d14c903c4a5b1cc538b20ab658fe30ab27c42be8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216368"
---
# <a name="filtering-raster-data"></a>筛选光栅数据





如果要在后台处理扫描行数据流之前提供其自定义的后处理，可以在[呈现插件](rendering-plug-ins.md)中实现[**IPrintOemUni：： FilterGraphics**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)方法来执行此操作。 没有与此 Unidrv 功能关联的 GPD 文件项。

有关详细信息，请参阅 [自定义数据流筛选](customized-data-stream-filtering.md)。

 

