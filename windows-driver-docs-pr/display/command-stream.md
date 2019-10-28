---
title: 命令流
description: 命令流
ms.assetid: 125e2072-42d6-4d4b-aec9-94b40a9d493c
keywords:
- Direct3D WDK Windows 2000 显示，操作代码
- 操作代码 WDK Direct3D
- 命令流 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc48b1d9a7be4776b964df9b76afa74bd59bd744
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839802"
---
# <a name="command-stream"></a>命令流


## <span id="ddk_command_stream_gg"></span><span id="DDK_COMMAND_STREAM_GG"></span>


在驱动程序级别，指令的形式为对[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)的调用。 输入结构[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)包含指向命令缓冲区的指针。 这是[**D3DHAL\_DP2COMMAND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2command)结构的序列。 其中每个结构都包含一个**bCommand**成员，该成员指定在缓冲区中跟随何种类型的数据。 此规范以[**D3DHAL\_DP2OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)枚举类型形式提供，例如 D3DDP2OP\_INDEXEDTRIANGLESTRIP，在设置纹理状态的情况下，D3DDP2OP\_TEXTURESTAGESTATE。

换句话说，D3DHAL\_DP2OPERATION 操作代码指定在命令缓冲区中跟随的结构类型。 要遵循的结构数由**wPrimitiveCount**或**wStateCount**指定，联合的成员将成为 D3DHAL\_DP2COMMAND 结构的成员。 **WPrimitiveCount**成员跟踪要呈现的图形基元数量，而**wStateCount**成员跟踪要处理的状态更改的数目。

有关驱动程序如何处理操作代码的示例，请参阅[处理纹理阶段](processing-texture-stages.md)。

 

 





