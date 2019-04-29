---
title: 光标
description: 光标
ms.assetid: 8647b0fc-b93b-489d-b2c0-b5caf98e800b
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，游标
- 游标 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd954bca92be289bc114c7f96b89586e1717d368
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370761"
---
# <a name="cursors"></a>光标


## <span id="ddk_cursors_gg"></span><span id="DDK_CURSORS_GG"></span>


DirectX 8.0 添加了一个 API，用于支持较高的更新频率游标，而无需 API 级别的直接访问到主图面。 DirectX 8.0 光标是标准的 GDI 游标，如果的功能允许，否则使用 DirectDraw blts 模拟。 若要支持 DirectX 游标 API，该驱动程序必须返回 D3DCAPS8 中功能的信息。

**CursorCaps**字段应设置为 D3DCURSORCAPS\_MONO、 D3DCURSORCAPS\_颜色，或两者，指示对于单色的支持和颜色硬件游标。 **MaxCursorEdgeSize**字段应设置为最大宽度的最小值和最大高度硬件游标 （或如果没有硬件游标支持为零）。 不能表示不同的最大大小的宽度和高度的光标。

 

 





