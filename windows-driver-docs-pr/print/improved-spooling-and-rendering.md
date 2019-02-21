---
title: 改进了后台处理和呈现
description: 改进了后台处理和呈现
ms.assetid: 0e385282-fbc8-4c4b-9070-19ee8290ddd6
keywords:
- XPSDrv 打印机驱动程序 WDK、 后台处理
- XPSDrv 打印机驱动程序 WDK、 呈现
- XPS 假脱机文件 WDK XPSDrv
- 打印后台打印文件 WDK
- 呈现插件 WDK 打印 XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fd249ee27c4d226fe45d0f45c1b61af2c6176a7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547798"
---
# <a name="improved-spooling-and-rendering"></a>改进了后台处理和呈现


XPS 打印路径提高了 XPS 后台打印文件格式的后台打印 XPS 文档的后台处理程序效率，当最终用户打印到 XPSDrv 的打印机驱动程序。 XPS 文档文件格式是 XPS 后台打印文件格式相同，因为后台处理过程的简化而来，无需生成中间后台打印文件，如增强型图元文件 (EMF) 数据文件，后台处理文档之前。 通过较小后台打印文件的大小，XPS 打印路径可以减少网络流量并提高打印性能。

EMF 是一种封闭的格式，它将一系列用于呈现服务再调用 GDI 的 GDI 调用表示应用程序输出。 与不同的 EMF，XPS 后台打印格式而无需进一步的转译，当目标 XPSDrv 驱动程序时表示实际可视化输出。 基于 GDI 的打印驱动程序要求数据和颜色空间转换，而的 XPSDrv 打印驱动程序可以直接对假脱机文件中的数据，从而避免这些转换。

使用 XPS 文档或目标 XPSDrv 驱动程序时，通常将降低后台打印文件的大小。 依赖于设备字体的文件和具有大型矢量内容的文件可能会导致更大的假脱机文件，但通常大幅降低后台打印文件。

通过在转换过程中的多个优化可以减小后台打印文件的大小：

-   对于所有字体子集的字体。 处理输出后，它包含用于在文件中的字体的字符。 这种优化极大地减少了假脱机文件对于文档，尤其是使用东亚字体集的文档的大小。

-   常见的资源，包括徽标和图像文件的标识。 转换过程确定是否映像已多次使用文档内，以及如果是这样，在 XPS 假脱机文件中创建的共享的资源。 这种优化可以显著减少假脱机文件对于需要进行大量图形的文档，如每张幻灯片使用相同的徽标和背景的 Microsoft PowerPoint 文件的大小。

-   ZIP 压缩。 ZIP 压缩实现为 XPS 后台打印文件格式 （XPS 文档格式） 的一部分。 这种优化减小后台打印文件的大小。

这些优化时随时 XPS 文档，或者创建 XPS 假脱机文件。

 

 




