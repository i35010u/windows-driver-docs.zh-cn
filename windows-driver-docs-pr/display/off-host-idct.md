---
title: 主机外 IDCT
description: 主机外 IDCT
ms.assetid: 31797487-0c4e-4b8c-801e-f545bd60cc6d
keywords:
- 宏块 WDK DirectX va，因此 IDCT
- 低级别 IDCT WDK DirectX VA
- 关闭主机 IDCT WDK DirectX VA
- 逆变离散余弦 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 564d6af5d6c73f6f84b2dfc73dc1b12cd75cdd29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372789"
---
# <a name="off-host-idct"></a>主机外 IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


完成非主机 IDCT 处理宏块逆变离散余弦值 (IDCT) 系数数据传输使用扫描索引和值信息的缓冲区来定义和指定的转换等式。 （尽管只有 6 位数量真正需要 8 x 8 转换块中），将作为 16 位字发送索引信息。 作为有符号 16 位字发送转换系数值信息 (尽管只有 12 位所需的 8 x 8 转换块的常见情况并*BPP*等于 8)。

转换中任意一种发送系数[ **DXVA\_TCoefSingle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_tcoefsingle)结构或[ **DXVA\_TCoef4Group**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_tcoef4group)结构。 如果**bConfig4GroupedCoefs**的成员[ **DXVA\_ConfigPictureDecode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_configpicturedecode)结构为零，则单独使用 DXVA发送系数\_TCoefSingle 结构。 如果**bConfig4GroupedCoefs**为 1，系数发送使用 DXVA 四个组\_TCoef4Group 结构。

 

 





