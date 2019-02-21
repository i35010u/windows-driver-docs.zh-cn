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
ms.openlocfilehash: 0200779d2e6f72317be85889cbcc40cb06fe8611
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543974"
---
# <a name="filtering-raster-data"></a>筛选光栅数据





如果你想要提供扫描行数据流中的自定义后续处理，它将处于假脱机之前，就可以做到通过实现[ **IPrintOemUni::FilterGraphics** ](https://msdn.microsoft.com/library/windows/hardware/ff554252)中的方法[呈现插件](rendering-plug-ins.md)。 没有与此 Unidrv 功能相关联 GPD 文件项。

有关详细信息，请参阅[自定义数据 Stream 筛选](customized-data-stream-filtering.md)。

 

 




