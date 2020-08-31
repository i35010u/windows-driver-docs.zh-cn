---
title: 用户裁剪平面
description: 用户裁剪平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- 剪辑飞机 WDK Direct3D
- 用户定义的剪辑平面 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9778f7aaf41fb50f6c9131aeeee24736372de139
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067160"
---
# <a name="user-clip-planes"></a>用户裁剪平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


为最新的 DirectX 版本启用用户定义的剪辑平面。 这些操作与其他剪辑平面的工作方式一样，但它们可由应用程序设置。 驱动程序必须通过响应 \_ [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)中的 D3DDP2OP SETCLIPPLANE 操作代码来处理这些平面。

 

