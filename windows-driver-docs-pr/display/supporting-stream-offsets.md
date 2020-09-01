---
title: 支持流偏移量
description: 支持流偏移量
ms.assetid: 2c2ca906-8685-47f5-a2ca-855394b9674f
keywords:
- 流偏移 WDK DirectX 9。0
- 顶点流偏移 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d449eac94fd5e5e3475199372bf4b08a37079e27
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064546"
---
# <a name="supporting-stream-offsets"></a>支持流偏移量


## <span id="ddk_supporting_stream_offsets_gg"></span><span id="DDK_SUPPORTING_STREAM_OFFSETS_GG"></span>


DirectX 9.0 版本驱动程序必须支持应用程序在单个顶点数据流中存储多个顶点格式的顶点数据。 应用程序通过向顶点数据的开头提供 *流偏移量*（以字节为单位），通知驱动程序特定格式的顶点数据位于顶点数据流中的位置。 若要支持流偏移，驱动程序必须 \_ 在其 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 函数中处理 D3DDP2OP SETSTREAMSOURCE2 操作代码。 [**D3DHAL \_ DP2SETSTREAMSOURCE2**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource2)结构（遵循[命令流](command-stream.md)中的操作代码）用于指定该流和顶点数据所在位置的偏移量。

 

