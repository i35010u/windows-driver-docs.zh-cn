---
title: 关闭主机 IDCT
description: 关闭主机 IDCT
ms.assetid: 31797487-0c4e-4b8c-801e-f545bd60cc6d
keywords:
- 宏块 WDK DirectX va，因此 IDCT
- 低级别 IDCT WDK DirectX VA
- 关闭主机 IDCT WDK DirectX VA
- 逆变离散余弦 WDK DirectX VA
- IDCT WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f05277f80d8d86a26702a8f089ab695acec40f87
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547918"
---
# <a name="off-host-idct"></a>关闭主机 IDCT


## <span id="_off_host_idct"></span><span id="_OFF_HOST_IDCT"></span>


完成非主机 IDCT 处理宏块逆变离散余弦值 (IDCT) 系数数据传输使用扫描索引和值信息的缓冲区来定义和指定的转换等式。 （尽管只有 6 位数量真正需要 8 x 8 转换块中），将作为 16 位字发送索引信息。 作为有符号 16 位字发送转换系数值信息 (尽管只有 12 位所需的 8 x 8 转换块的常见情况并*BPP*等于 8)。

转换中任意一种发送系数[ **DXVA\_TCoefSingle** ](https://msdn.microsoft.com/library/windows/hardware/ff564060)结构或[ **DXVA\_TCoef4Group**](https://msdn.microsoft.com/library/windows/hardware/ff564053)结构。 如果**bConfig4GroupedCoefs**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构为零，则单独使用 DXVA发送系数\_TCoefSingle 结构。 如果**bConfig4GroupedCoefs**为 1，系数发送使用 DXVA 四个组\_TCoef4Group 结构。

 

 





