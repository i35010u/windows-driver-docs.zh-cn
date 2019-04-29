---
title: 自定义的数据流筛选
description: 自定义的数据流筛选
ms.assetid: 768d4b95-4d8d-4460-9a8c-c80785f7f799
keywords:
- Unidrv，流筛选数据
- 数据流筛选 WDK Unidrv
- 筛选 WDK Unidrv 的自定义的数据流
- 筛选 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7a6c4f2681062f9f3cbb76b03765c8ace093e1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365551"
---
# <a name="customized-data-stream-filtering"></a>自定义的数据流筛选





Unidrv 允许自定义的代码之前它将处于假脱机执行的图像数据的最终后处理。 删除相邻点或筛选操作 Unidrv 不提供任何其他数据可能包含此类处理。

若要执行最终的后续处理的图像数据，提供插件的呈现实现[ **IPrintOemUni::FilterGraphics** ](https://msdn.microsoft.com/library/windows/hardware/ff554252)方法。

[ **IPrintOemUni::FilterGraphics** ](https://msdn.microsoft.com/library/windows/hardware/ff554252)方法接收扫描的行数据作为输入。 方法必须处理的数据，然后将其发送到打印后台处理程序通过调用[ **IPrintOemDriverUni::DrvWriteSpoolBuf**](https://msdn.microsoft.com/library/windows/hardware/ff553138)。 如果**IPrintOemUni::FilterGraphics**方法的实现、 Unidrv 不后台打印打印机的数据。 相反，它将发送到每个数据块**IPrintOemUni::FilterGraphics**方法。

 

 




