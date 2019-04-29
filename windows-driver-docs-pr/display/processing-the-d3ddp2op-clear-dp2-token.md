---
title: 处理 D3DDP2OP_CLEAR DP2 标记
description: 处理 D3DDP2OP_CLEAR DP2 标记
ms.assetid: ec027f44-bdd5-4d5a-8c47-1ac6a0c1cb6e
keywords:
- DirectX 8.0 版本显示说明 WDK Windows 2000，纯设备 D3DDP2OP_CLEAR DP2 令牌处理
- 纯设备 WDK DirectX 8.0，D3DDP2OP_CLEAR DP2 令牌处理
- D3DDP2OP_CLEAR WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b29b010e9b38d0a5a5ecd3d29dae392b80dea11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383888"
---
# <a name="processing-the-d3ddp2opclear-dp2-token"></a>处理 D3DDP2OP\_清除 DP2 令牌


## <span id="ddk_processing_the_d3ddp2op_clear_dp2_token_gg"></span><span id="DDK_PROCESSING_THE_D3DDP2OP_CLEAR_DP2_TOKEN_GG"></span>


DirectX 8.0 引入了一些更改为所需的处理的 D3DDP2OP\_清除标记。 特别是新标志 D3DCLEAR\_已添加到 COMPUTERECTS **dwFlags**字段[ **D3DHAL\_DP2CLEAR** ](https://msdn.microsoft.com/library/windows/hardware/ff545441)数据结构。 此新标志仅传递给驱动程序，在使用纯设备类型时 (即，D3DCREATE\_时创建的设备和驱动程序导出 D3DDEVCAPS 指定 PUREDEVICE\_PUREDEVICE 达到设备上限)。 此外，此标志永远不会传递给非 DirectX 8.0 驱动程序并不由使用旧**清晰**或**Clear2**驱动程序回调。

 

 





