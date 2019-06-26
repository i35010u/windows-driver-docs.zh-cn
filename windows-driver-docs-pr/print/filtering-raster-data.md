---
title: 筛选光栅数据
description: 筛选光栅数据
ms.assetid: 179a2dc0-8794-4934-99b9-eb3f7900536c
keywords:
- Unidrv，光栅数据筛选
- GPD 文件 WDK Unidrv，光栅数据筛选
- 筛选光栅数据 WDK 打印
- 光栅数据筛选 WDK Unidrv
- 后续处理扫描的行数据流 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f5a25a6a9207d8f2af551f8c0dcc481f424b8d4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382568"
---
# <a name="filtering-raster-data"></a>筛选光栅数据





如果你想要提供扫描行数据流中的自定义后续处理，它将处于假脱机之前，就可以做到通过实现[ **IPrintOemUni::FilterGraphics** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)中的方法[呈现插件](rendering-plug-ins.md)。 没有与此 Unidrv 功能相关联 GPD 文件项。

有关详细信息，请参阅[自定义数据 Stream 筛选](customized-data-stream-filtering.md)。

 

 




