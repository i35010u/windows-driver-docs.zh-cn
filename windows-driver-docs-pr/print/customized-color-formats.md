---
title: 自定义的颜色格式
description: 自定义的颜色格式
ms.assetid: 309d33e8-6338-4c32-8e03-d6cbf3371e16
keywords:
- Unidrv，颜色格式
- 颜色格式 WDK Unidrv
- 自定义颜色格式 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f2125aa3e39e8a9382d8b01b65e378f08d1c5bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842847"
---
# <a name="customized-color-formats"></a>自定义的颜色格式





Unidrv 支持多种颜色格式，这些颜色格式在[处理颜色格式](handling-color-formats.md)中列出。 对于这些格式，Unidrv 将 GDI 位图转换为正确的格式，然后将其发送到打印机。 如果打印机接受 Unidrv 不支持的格式，则必须提供实现[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)方法的呈现插件。

如果实现[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)，并且用户选择了 Unidrv 无法处理的颜色格式（ColorMode 选项），则在每次将 GDI 位图数据的缓冲区准备好进行打印时，Unidrv 将调用方法并传递位图的地址作为输入参数。 方法必须将位图转换为指定的格式、执行[自定义的半色调](customized-halftoning.md)操作（如有必要），并调用[**IPrintOemDriverUni：:D rvwritespoolbuf**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)方法将修改后的位图发送到打印后台处理程序。 它还必须调用[**IPrintOemDriverUni：:D rvxmoveto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto)和[**IPrintOemDriverUni：:D rvymoveto**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto)方法来更新游标位置。 有关这些操作的详细信息，请参阅**IPrintOemUni：： ImageProcessing**的说明。

如果呈现插件实现[**IPrintOemUni：： ImageProcessing**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)，它还可以实现[**IPrintOemUni：： MemoryUsage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)。

 

 




