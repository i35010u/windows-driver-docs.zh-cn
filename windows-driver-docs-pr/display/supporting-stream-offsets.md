---
title: 支持流偏移量
description: 支持流偏移量
ms.assetid: 2c2ca906-8685-47f5-a2ca-855394b9674f
keywords:
- 流偏移量 WDK DirectX 9.0
- 顶点流偏移量 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3117ab6b50f90079661f901ab276180651f12e46
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361245"
---
# <a name="supporting-stream-offsets"></a>支持流偏移量


## <span id="ddk_supporting_stream_offsets_gg"></span><span id="DDK_SUPPORTING_STREAM_OFFSETS_GG"></span>


DirectX 9.0 版本驱动程序必须支持让应用程序将多个顶点格式的顶点数据存储在单个顶点数据流。 应用程序通知特定格式的顶点数据所处位置的顶点数据流中提供的驱动程序*流偏移量*，以字节为单位，这些顶点数据的开头。 若要支持流偏移量，该驱动程序必须处理 D3DDP2OP\_SETSTREAMSOURCE2 操作代码中其[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数。 一个[ **D3DHAL\_DP2SETSTREAMSOURCE2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource2)结构，该过程中的操作代码[命令流](command-stream.md)，用于指定的流和到的偏移量顶点数据所在的位置。

 

 





