---
title: 改进的后台打印和渲染
description: 改进的后台打印和渲染
keywords:
- XPSDrv 打印机驱动程序 WDK，假脱机
- XPSDrv 打印机驱动程序 WDK，呈现
- XPS 假脱机文件 WDK XPSDrv
- 假脱机文件 WDK 打印
- 呈现插件 WDK 打印，XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3653a3a723605333f1ee37c97e1913acfafb3ad8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796755"
---
# <a name="improved-spooling-and-rendering"></a>改进的后台打印和渲染


当最终用户打印到 XPSDrv 打印机驱动程序时，XPS 打印路径通过以 XPS 假脱机文件格式对 XPS 文档进行后台打印，从而提高了后台处理程序的效率。 由于 XPS 文档文件格式与 XPS 假脱机文件格式相同，因此简化了假脱机过程，并且不需要在文档进行后台处理之前生成中间后台打印文件（如增强型图元文件 (EMF) 数据文件）。 通过较小的假脱机文件大小，XPS 打印路径可以减少网络流量并提高打印性能。

EMF 是一种封闭格式，它将应用程序输出表示为一系列 GDI 调用，然后需要调用 GDI 以呈现服务。 与 EMF 不同，XPS 假脱机格式表示实际的视觉对象输出，而不需要在面向 XPSDrv 驱动程序时进行进一步解释。 基于 GDI 的打印驱动程序需要数据和颜色空间转换，而 XPSDrv 打印驱动程序可以直接对假脱机文件中的数据进行操作，避免这些转换。

使用 XPS 文档或以 XPSDrv 驱动程序为目标时，通常会降低假脱机文件的大小。 依赖于设备字体和包含大型矢量内容的文件的文件可能会导致后台打印文件较大，但后台打印文件的大小通常较小。

在转换过程中，假脱机文件的大小经过多种优化：

-   所有字体的字体子集。 处理输出后，只包含文件中的字体所使用的字符。 此优化极大地减小了文档的假脱机文件大小，尤其是使用中文字体集的文档。

-   常见资源（包括徽标和图像文件）的标识。 转换过程标识某个图像是否在文档中多次使用，如果是，则在 XPS 假脱机文件中创建一个共享资源。 此优化可显著减少图形密集型文档（例如，在每个幻灯片上使用相同徽标和背景的 Microsoft PowerPoint 文件）的后台处理文件的大小。

-   ZIP 压缩。 ZIP 压缩作为 XPS 假脱机文件格式的一部分实现 (XPS 文档格式) 。 此优化降低了假脱机文件的大小。

无论何时创建 XPS 文档或 XPS 假脱机文件，都会进行这些优化。

 

 




