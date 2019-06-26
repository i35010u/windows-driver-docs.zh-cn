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
ms.openlocfilehash: 1aa0d709eff31f60608734c3e7a7e9d2e6780f0a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381882"
---
# <a name="extended-blt-flags"></a>扩展的 Blt 标志


## <span id="ddk_extended_blt_flags_gg"></span><span id="DDK_EXTENDED_BLT_FLAGS_GG"></span>


DirectX 9.0 使用 DDBLT\_扩展\_标志 blt 标志来扩展使用 DDBLT\_*Xxx* blt 标志，它们位于**dwFlags** 成员[ **DD\_BLTDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_bltdata)结构。 当 DirectX 9.0 运行时调用显示器驱动程序[ *DdBlt* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数来执行 blt 操作中，运行时可以组合 DDBLT\_扩展\_DDBLT的标志\_*Xxx*标志使用位或运算来创建新的含义的标志。 该驱动程序然后确定是否存在 DDBLT\_扩展\_标志，重新解释的标志的含义，并相应地执行 blt 操作。 驱动程序时它会确定是否它应使用此机制[执行灰度校正](performing-gamma-correction-on-swap-chains.md)期间从后台缓冲区到桌面 blt 线性颜色空间上。 驱动程序还使用扩展的 blt 标志确定是否[延伸 blit 操作](supporting-stretch-blit-operations.md)请求。

 

 





