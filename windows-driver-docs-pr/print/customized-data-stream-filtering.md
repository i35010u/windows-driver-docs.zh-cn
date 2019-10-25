---
title: 自定义的数据流筛选
description: 自定义的数据流筛选
ms.assetid: 768d4b95-4d8d-4460-9a8c-c80785f7f799
keywords:
- Unidrv，数据流筛选
- 数据流筛选 WDK Unidrv
- 自定义的数据流筛选 WDK Unidrv
- 筛选 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ac5b6962c59394030af7f38b864ff237432bccd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837980"
---
# <a name="customized-data-stream-filtering"></a>自定义的数据流筛选





Unidrv 允许自定义代码在后台处理图像数据之前对其执行最终后处理。 此类处理可能包含删除相邻点或 Unidrv 未提供的任何其他数据筛选操作。

若要执行图像数据的最终后处理，请提供实现[**IPrintOemUni：： FilterGraphics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)方法的呈现插件。

[**IPrintOemUni：： FilterGraphics**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)方法接收扫描行数据作为输入。 方法必须处理数据，然后通过调用[**IPrintOemDriverUni：:D rvwritespoolbuf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)将其发送到打印后台处理程序。 如果实现了**IPrintOemUni：： FilterGraphics**方法，则 Unidrv 不会后台打印数据。 相反，它会将每个数据块发送到**IPrintOemUni：： FilterGraphics**方法。

 

 




