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
ms.openlocfilehash: defe91a6900530cb05349f939b5253de4f628f67
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063846"
---
# <a name="off-host-idct"></a>主机外 IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


使用扫描索引和值信息的缓冲区传输宏块反离散-余弦转换 (IDCT) 系数数据来定义和指定转换等式。 索引信息以16位字的形式发送 (虽然只需6位数量的8x8 转换块) 。 转换系数值信息将作为有符号的16位字发送 (虽然通常情况下，8x8 变换块和 *BPP* 等于 8) 只需要12位。

转换系数在 [**DXVA \_ TCoefSingle**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoefsingle) 结构或 [**DXVA \_ TCoef4Group**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoef4group) 结构中发送。 如果[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**bConfig4GroupedCoefs**成员为零，则将使用 DXVA TCoefSingle 结构分别发送系数 \_ 。 如果 **bConfig4GroupedCoefs** 为1，则将使用 DXVA TCoef4Group 结构按四组的系数发送系数 \_ 。

 

