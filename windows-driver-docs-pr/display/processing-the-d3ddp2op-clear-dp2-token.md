---
title: 处理 D3DDP2OP_CLEAR DP2 标记
description: 处理 D3DDP2OP_CLEAR DP2 标记
ms.assetid: ec027f44-bdd5-4d5a-8c47-1ac6a0c1cb6e
keywords:
- DirectX 8.0 发行说明，WDK Windows 2000 显示，纯粹设备，D3DDP2OP_CLEAR DP2 令牌处理
- 纯设备 WDK DirectX 8.0，D3DDP2OP_CLEAR DP2 令牌处理
- D3DDP2OP_CLEAR WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a200a85af8b712b72fa40eac63a765a67663f18
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829684"
---
# <a name="processing-the-d3ddp2op_clear-dp2-token"></a>处理 D3DDP2OP\_清除 DP2 标记


## <span id="ddk_processing_the_d3ddp2op_clear_dp2_token_gg"></span><span id="DDK_PROCESSING_THE_D3DDP2OP_CLEAR_DP2_TOKEN_GG"></span>


DirectX 8.0 对 D3DDP2OP\_CLEAR 标记所需的处理进行了一些更改。 具体而言，已将新的标志\_D3DCLEAR 添加到[**D3DHAL\_DP2CLEAR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2clear)数据结构的**dwFlags**字段。 仅当使用纯设备类型时（即，在创建设备时指定了 D3DCREATE\_PUREDEVICE，驱动程序将导出 D3DDEVCAPS\_PUREDEVICE 设备 cap）时，才会将此新标志传递给驱动程序。 此外，此标志绝不会传递到非 DirectX 8.0 驱动程序，也不会使用旧的**Clear**或**Clear2**驱动程序回调来指定它。

 

 





