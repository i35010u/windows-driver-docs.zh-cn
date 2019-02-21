---
title: 扩展盘区调整
description: 扩展盘区调整
ms.assetid: b3562744-375a-4d6f-be09-e28314282faa
keywords:
- Direct3D WDK Windows 2000 显示，扩展盘区调整
- 扩展盘区调整 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7aa4b75f3c6d50e75a3383e4793c9a8749d59882
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519243"
---
# <a name="extents-adjustment"></a>扩展盘区调整


## <span id="ddk_extents_adjustment_gg"></span><span id="DDK_EXTENTS_ADJUSTMENT_GG"></span>


某些硬件使用影响像素的屏幕空间顶点定义的扩展盘区矩形之外的抗锯齿内核。 使用扩展盘区矩形 D3DCLIPSTATUS 结构中的应用程序 (在中定义*d3dtypes.h*) 的已更新矩形处理可能会呈现项目，因为该扩展盘区矩形不涉及像素修改的硬件。

Direct3D 硬件驱动程序以请求扩展盘区矩形进行向外调整为指定的中的像素数，从而解决了此问题**dvExtentsAdjust**的成员[ **D3DHAL\_D3DEXTENDEDCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff544753)结构。 此成员填充以响应 GUID\_D3DExtendedCaps GUID [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)。 扩展盘区矩形剪辑到的盘区的设备将呈现器目标图面中。 默认值为 0。

 

 





