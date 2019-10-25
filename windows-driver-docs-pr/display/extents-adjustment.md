---
title: 范围调整
description: 范围调整
ms.assetid: b3562744-375a-4d6f-be09-e28314282faa
keywords:
- Direct3D WDK Windows 2000 显示，区调整
- 区调整 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c06790f1507db5df060949eca10496422b0d7dec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839696"
---
# <a name="extents-adjustment"></a>范围调整


## <span id="ddk_extents_adjustment_gg"></span><span id="DDK_EXTENTS_ADJUSTMENT_GG"></span>


某些硬件使用抗锯齿内核，该内核影响屏幕空间顶点定义的区的范围。 使用 D3DCLIPSTATUS 结构（在*d3dtypes*中定义）进行脏矩形处理的应用程序可能会遇到渲染项目，因为区矩形不涵盖硬件修改的像素。

Direct3D 通过以下方式解决此问题：允许硬件驱动程序请求在[**D3DHAL\_D3DEXTENDEDCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_d3dextendedcaps)结构的**dvExtentsAdjust**成员中，将范围矩形向外调整到指定的像素数。 此成员是为响应[**DdGetDriverInfo**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)中的 Guid\_D3DExtendedCaps guid 而填充的。 区矩形被剪裁到设备的呈现器目标表面的范围。 默认值为 0。

 

 





