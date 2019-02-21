---
title: 支持 Stream 偏移量
description: 支持 Stream 偏移量
ms.assetid: 2c2ca906-8685-47f5-a2ca-855394b9674f
keywords:
- 流偏移量 WDK DirectX 9.0
- 顶点流偏移量 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c4795f469ed5759d11a971f288a6f15e44f5d93
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544291"
---
# <a name="supporting-stream-offsets"></a>支持 Stream 偏移量


## <span id="ddk_supporting_stream_offsets_gg"></span><span id="DDK_SUPPORTING_STREAM_OFFSETS_GG"></span>


DirectX 9.0 版本驱动程序必须支持让应用程序将多个顶点格式的顶点数据存储在单个顶点数据流。 应用程序通知特定格式的顶点数据所处位置的顶点数据流中提供的驱动程序*流偏移量*，以字节为单位，这些顶点数据的开头。 若要支持流偏移量，该驱动程序必须处理 D3DDP2OP\_SETSTREAMSOURCE2 操作代码中其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数。 一个[ **D3DHAL\_DP2SETSTREAMSOURCE2** ](https://msdn.microsoft.com/library/windows/hardware/ff545801)结构，该过程中的操作代码[命令流](command-stream.md)，用于指定的流和到的偏移量顶点数据所在的位置。

 

 





