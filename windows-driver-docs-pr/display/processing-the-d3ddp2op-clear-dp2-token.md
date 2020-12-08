---
title: 处理 D3DDP2OP_CLEAR DP2 标记
description: 处理 D3DDP2OP_CLEAR DP2 标记
keywords:
- DirectX 8.0 发行说明了 WDK Windows 2000 显示、纯设备 D3DDP2OP_CLEAR DP2 令牌处理
- 纯设备 WDK DirectX 8.0，D3DDP2OP_CLEAR DP2 令牌处理
- D3DDP2OP_CLEAR WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3526506a04dfeaf175d3e182d1090a6e67b9141b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792949"
---
# <a name="processing-the-d3ddp2op_clear-dp2-token"></a>处理 D3DDP2OP \_ CLEAR DP2 标记


## <span id="ddk_processing_the_d3ddp2op_clear_dp2_token_gg"></span><span id="DDK_PROCESSING_THE_D3DDP2OP_CLEAR_DP2_TOKEN_GG"></span>


DirectX 8.0 引入了对所需的 D3DDP2OP CLEAR 标记处理的一些更改 \_ 。 具体而言，已将一个新的标志 D3DCLEAR \_ COMPUTERECTS 添加到 [**D3DHAL \_ DP2CLEAR**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2clear)数据结构的 **dwFlags** 字段。 仅当使用纯设备类型时，才会将此新标志传递到驱动程序 (即，在 \_ 创建设备时指定了 D3DCREATE PUREDEVICE，驱动程序将导出 D3DDEVCAPS \_ PUREDEVICE 设备 cap) 。 此外，此标志绝不会传递到非 DirectX 8.0 驱动程序，也不会使用旧的 **Clear** 或 **Clear2** 驱动程序回调来指定它。

 

