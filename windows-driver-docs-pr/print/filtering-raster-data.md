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
ms.openlocfilehash: 5c243056b874d0fdb6fc2af9b1885b77dcbf11b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833834"
---
# <a name="filtering-raster-data"></a>筛选光栅数据





如果要在后台处理扫描行数据流之前提供其自定义的后处理，可以在[呈现插件](rendering-plug-ins.md)中实现[**IPrintOemUni：： FilterGraphics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)方法来执行此操作。 没有与此 Unidrv 功能关联的 GPD 文件项。

有关详细信息，请参阅[自定义数据流筛选](customized-data-stream-filtering.md)。

 

 




