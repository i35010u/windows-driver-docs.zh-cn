---
title: 扩展的 Blt 标志
description: 扩展的 Blt 标志
ms.assetid: 9c2f7013-dd58-4a61-b452-d263f5caf0d0
keywords:
- 扩展的 blt 标志 WDK DirectX 9.0
- DDBLT_EXTENDED_FLAGS
- blt 标志扩展 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c19ba45ea4eee42f5220540a5ea04d337c8d6e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522661"
---
# <a name="extended-blt-flags"></a>扩展的 Blt 标志


## <span id="ddk_extended_blt_flags_gg"></span><span id="DDK_EXTENDED_BLT_FLAGS_GG"></span>


DirectX 9.0 使用 DDBLT\_扩展\_标志 blt 标志来扩展使用 DDBLT\_*Xxx* blt 标志，它们位于**dwFlags** 成员[ **DD\_BLTDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550474)结构。 当 DirectX 9.0 运行时调用显示器驱动程序[ *DdBlt* ](https://msdn.microsoft.com/library/windows/hardware/ff549205)函数来执行 blt 操作中，运行时可以组合 DDBLT\_扩展\_DDBLT的标志\_*Xxx*标志使用位或运算来创建新的含义的标志。 该驱动程序然后确定是否存在 DDBLT\_扩展\_标志，重新解释的标志的含义，并相应地执行 blt 操作。 驱动程序时它会确定是否它应使用此机制[执行灰度校正](performing-gamma-correction-on-swap-chains.md)期间从后台缓冲区到桌面 blt 线性颜色空间上。 驱动程序还使用扩展的 blt 标志确定是否[延伸 blit 操作](supporting-stretch-blit-operations.md)请求。

 

 





