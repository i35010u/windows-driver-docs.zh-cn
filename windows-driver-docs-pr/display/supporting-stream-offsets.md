---
title: 支持流偏移量
description: 支持流偏移量
ms.assetid: 2c2ca906-8685-47f5-a2ca-855394b9674f
keywords:
- 流偏移 WDK DirectX 9。0
- 顶点流偏移 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a48186483c0c28784170af69d29b73d5696277e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829381"
---
# <a name="supporting-stream-offsets"></a>支持流偏移量


## <span id="ddk_supporting_stream_offsets_gg"></span><span id="DDK_SUPPORTING_STREAM_OFFSETS_GG"></span>


DirectX 9.0 版本驱动程序必须支持应用程序在单个顶点数据流中存储多个顶点格式的顶点数据。 应用程序通过向顶点数据的开头提供*流偏移量*（以字节为单位），通知驱动程序特定格式的顶点数据位于顶点数据流中的位置。 若要支持流偏移，驱动程序必须在其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数中处理 D3DDP2OP\_SETSTREAMSOURCE2 操作代码。 [**D3DHAL\_DP2SETSTREAMSOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource2)结构（遵循[命令流](command-stream.md)中的操作代码）用于指定该流和顶点数据所在位置的偏移量。

 

 





