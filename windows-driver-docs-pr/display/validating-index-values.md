---
title: 验证索引值
description: 验证索引值
ms.assetid: 09247df3-0c87-48cf-9c94-bda23c6b38d2
keywords:
- 用户模式显示驱动程序 WDK Windows Vista 中，索引验证
- 验证显示 WDK 的索引值
- 索引验证 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7c563aaed8960f877a669b0f0445aadcc07b1de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373554"
---
# <a name="validating-index-values"></a>验证索引值


用户模式显示驱动程序可以传递"而设计的 Microsoft Windows"硬件徽标测试，而不考虑它是否执行索引的验证。 但是，若要确保该驱动程序可使用 Microsoft DirectX 的应用程序可能传递无效的索引，用户模式显示驱动程序应执行索引验证。

应考虑以下各项：

-   在呈现与顶点缓冲区时，DirectX 8.0 和 DirectX 9.0 应用程序可以传递 stride 值为 0。 在此情况下，应引用仅顶点 0。 Stride 值中设置**Stride**的成员[ **D3DDDIARG\_SETSTREAMSOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_setstreamsource)中对用户模式显示驱动程序的结构[ **SetStreamSource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsource)函数。

-   驱动程序的调用[ **SetStreamSourceUM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsourceum)函数不包括的顶点数据的大小。 也就是说，提供的顶点数据的用户内存缓冲区的大小， *pUMBuffer*的参数*SetStreamSourceUM*指向未指定。

-   **NumVertices**的成员[ **D3DDDIARG\_DRAWINDEXEDPRIMITIVE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive)或[ **D3DDDIARG\_DRAWINDEXEDPRIMITIVE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive2)结构永远不会设置为 0，驱动程序的调用中[ **DrawIndexedPrimitive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive)或者[ **DrawIndexedPrimitive2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive2)函数。 该驱动程序应设置为允许的最大索引 (NumVerticesÂ--1)。

 

 





