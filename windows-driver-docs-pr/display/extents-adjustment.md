---
title: 范围调整
description: 范围调整
keywords:
- Direct3D WDK Windows 2000 显示，区调整
- 区调整 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51626d2a4feb157da16cadaa49f73a2ebc8d460
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827319"
---
# <a name="extents-adjustment"></a>范围调整


## <span id="ddk_extents_adjustment_gg"></span><span id="DDK_EXTENTS_ADJUSTMENT_GG"></span>


某些硬件使用抗锯齿内核，该内核影响屏幕空间顶点定义的区的范围。 在 D3DCLIPSTATUS 结构中使用区矩形的应用程序 (在) *d3dtypes* 中定义的用于脏矩形处理的应用程序可能会遇到渲染项目，因为区矩形不涵盖硬件修改的像素。

Direct3D 通过以下方式解决此问题：允许硬件驱动程序请求在 [**D3DHAL \_ D3DEXTENDEDCAPS**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)结构的 **dvExtentsAdjust** 成员中，将范围矩形向外调整到指定的像素数。 此成员将被填充为对 \_ [**DdGetDriverInfo**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)中的 guid D3DExtendedCaps guid 的响应。 区矩形被剪裁到设备的呈现器目标表面的范围。 默认值为零。

 

