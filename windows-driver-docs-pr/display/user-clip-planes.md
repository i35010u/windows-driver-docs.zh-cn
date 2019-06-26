---
title: 用户裁剪平面
description: 用户裁剪平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- 剪辑平面 WDK Direct3D
- 用户定义的剪辑平面 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef90b1ca0ee195d96df5b8cf3268a165cd43673d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373613"
---
# <a name="user-clip-planes"></a>用户裁剪平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


用户定义的剪辑平面启用最新版本的 DirectX 版本。 这些工作原理与其他剪辑平面，但它们是可由应用程序设置。 该驱动程序必须处理这些平面回应 D3DDP2OP\_SETCLIPPLANE 操作代码中[ **D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)。

 

 





