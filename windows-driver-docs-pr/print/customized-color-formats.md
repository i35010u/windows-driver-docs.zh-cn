---
title: 自定义的颜色格式
description: 自定义的颜色格式
keywords:
- Unidrv，颜色格式
- 颜色格式 WDK Unidrv
- 自定义颜色格式 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b2746dc1af1480cdef059169e49cb0d6f7ed27c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797423"
---
# <a name="customized-color-formats"></a>自定义的颜色格式





Unidrv 支持多种颜色格式，这些颜色格式在 [处理颜色格式](handling-color-formats.md)中列出。 对于这些格式，Unidrv 将 GDI 位图转换为正确的格式，然后将其发送到打印机。 如果打印机接受 Unidrv 不支持的格式，则必须提供实现 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing) 方法的呈现插件。

如果实现 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)，并且用户选择了一个颜色格式 (ColorMode 选项) 该 Unidrv 无法处理，则每次 GDI 位图数据的缓冲区都可以进行打印时，Unidrv 将调用方法，并将该位图的地址作为输入参数传递。 方法必须将位图转换为指定的格式、执行 [自定义的半色调](customized-halftoning.md) 操作（如有必要），并调用 [**IPrintOemDriverUni：:D rvwritespoolbuf**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf) 方法将修改后的位图发送到打印后台处理程序。 它还必须调用 [**IPrintOemDriverUni：:D rvxmoveto**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto) 和 [**IPrintOemDriverUni：:D rvymoveto**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto) 方法来更新游标位置。 有关这些操作的详细信息，请参阅 **IPrintOemUni：： ImageProcessing** 的说明。

如果呈现插件实现 [**IPrintOemUni：： ImageProcessing**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)，它还可以实现 [**IPrintOemUni：： MemoryUsage**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)。

 

