---
title: 用户裁剪平面
description: 用户裁剪平面
keywords:
- 剪辑飞机 WDK Direct3D
- 用户定义的剪辑平面 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3028efc28a431e68d9ef94c11531c44b7ffe85f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802531"
---
# <a name="user-clip-planes"></a>用户裁剪平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


为最新的 DirectX 版本启用用户定义的剪辑平面。 这些操作与其他剪辑平面的工作方式一样，但它们可由应用程序设置。 驱动程序必须通过响应 \_ [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)中的 D3DDP2OP SETCLIPPLANE 操作代码来处理这些平面。

 

