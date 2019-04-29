---
title: W 缓冲 DDI
description: W 缓冲 DDI
ms.assetid: eb1270c3-0eaa-47a4-8fc6-53aea981b597
keywords:
- Direct3D WDK Windows 2000 显示、 w 缓冲
- w 缓冲 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 162a51e816114945fb1824fcd6713e90fa0fba3a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391203"
---
# <a name="w-buffering-ddi"></a>W 缓冲 DDI


## <span id="ddk_w_buffering_ddi_gg"></span><span id="DDK_W_BUFFERING_DDI_GG"></span>


该驱动程序支持 w 缓冲，从而 D3DPRASTERCAPS\_中的 WBUFFER cap **dwRasterCaps**的成员[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)结构。 D3DRENDERSTATE\_w 缓冲或 z 缓冲 ZENABLE 呈现状态传递到要启用或禁用的驱动程序。

[ **D3DHAL\_DP2VIEWPORTINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff545936)结构支持平面与世界空间前端和后剪辑相对应的字段 (hither 和 yon 分别)。 此信息可用于调整雾的表。

 

 





