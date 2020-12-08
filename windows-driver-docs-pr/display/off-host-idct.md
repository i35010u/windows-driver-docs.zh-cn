---
title: 主机外 IDCT
description: 主机外 IDCT
keywords:
- macroblocks WDK DirectX VA，IDCT
- 低级别 IDCT WDK DirectX VA
- 脱离主机 IDCT WDK DirectX VA
- 逆离散-余弦转换 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7416fd152282664f68f4b9a256eaf1cb765c7be0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828077"
---
# <a name="off-host-idct"></a>主机外 IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


使用扫描索引和值信息的缓冲区传输宏块反离散-余弦转换 (IDCT) 系数数据来定义和指定转换等式。 索引信息以16位字的形式发送 (虽然只需6位数量的8x8 转换块) 。 转换系数值信息将作为有符号的16位字发送 (虽然通常情况下，8x8 变换块和 *BPP* 等于 8) 只需要12位。

转换系数在 [**DXVA \_ TCoefSingle**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoefsingle) 结构或 [**DXVA \_ TCoef4Group**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_tcoef4group) 结构中发送。 如果 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的 **bConfig4GroupedCoefs** 成员为零，则将使用 DXVA TCoefSingle 结构分别发送系数 \_ 。 如果 **bConfig4GroupedCoefs** 为1，则将使用 DXVA TCoef4Group 结构按四组的系数发送系数 \_ 。

 

