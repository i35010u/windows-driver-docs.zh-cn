---
title: 验证索引值
description: 验证索引值
ms.assetid: 09247df3-0c87-48cf-9c94-bda23c6b38d2
keywords:
- 用户模式显示驱动程序 WDK Windows Vista，索引验证
- 验证索引值 WDK 显示
- 索引验证 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5a9e0d185720dbcb47f16af386d3f2f7c5a2a6b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067054"
---
# <a name="validating-index-values"></a>验证索引值


用户模式显示驱动程序可以为硬件徽标测试传递 "设计用于 Microsoft Windows"，而不管是否执行索引验证。 但是，为了确保驱动程序适用于可能传递无效索引的 Microsoft DirectX 应用程序，用户模式显示驱动程序应执行索引验证。

应考虑以下事项：

-   当使用顶点缓冲区呈现时，DirectX 8.0 和 DirectX 9.0 应用程序可以传递步幅值0。 在这种情况下，只应引用顶点0。 跨距值是在对用户模式显示驱动程序的[**SETSTREAMSOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsource)函数的调用中，在[**D3DDDIARG \_ SETSTREAMSOURCE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_setstreamsource)结构的**stride**成员中设置的。

-   对驱动程序的 [**SetStreamSourceUM**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_setstreamsourceum) 函数的调用不包括顶点数据的大小。 即，用户内存缓冲区的大小，该缓冲区提供未指定*SetStreamSourceUM*指向的*pUMBuffer*参数的顶点数据。

-   调用驱动程序的[**DRAWINDEXEDPRIMITIVE2**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive)或[**DRAWINDEXEDPRIMITIVE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_drawindexedprimitive2)函数时， [**D3DDDIARG \_ DRAWINDEXEDPRIMITIVE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive)或[**D3DDDIARG \_ DRAWINDEXEDPRIMITIVE2**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_drawindexedprimitive2)结构的**NumVertices**成员从不设置为0。 驱动程序应将允许的最大索引设置为 (NumVerticesÂ-1) 。

 

