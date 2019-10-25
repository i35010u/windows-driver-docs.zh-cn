---
title: 主机外 IDCT
description: 主机外 IDCT
ms.assetid: 31797487-0c4e-4b8c-801e-f545bd60cc6d
keywords:
- macroblocks WDK DirectX VA，IDCT
- 低级别 IDCT WDK DirectX VA
- 脱离主机 IDCT WDK DirectX VA
- 逆离散-余弦转换 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 749c9e1bc5cf2cf2db7666c8eed630976f9d85f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840506"
---
# <a name="off-host-idct"></a>主机外 IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


对于脱离主机 IDCT 处理，宏块反离散-余弦转换（IDCT）系数数据的传输使用扫描索引和值信息的缓冲区来定义和指定转换公式。 索引信息以16位字的形式发送（尽管8x8 转换块仅需6位数量）。 转换系数值信息发送为有符号的16位字（尽管通常情况下，8x8 转换块和*BPP*等于8的情况下仅需要12位）。

转换系数在[**DXVA\_TCoefSingle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoefsingle)结构或[**DXVA\_TCoef4Group**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoef4group)结构中发送。 如果[**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfig4GroupedCoefs**成员为零，则使用 DXVA\_TCoefSingle 结构分别发送系数。 如果**bConfig4GroupedCoefs**为1，则将使用 DXVA\_TCoef4Group 结构按四组的系数发送系数。

 

 





