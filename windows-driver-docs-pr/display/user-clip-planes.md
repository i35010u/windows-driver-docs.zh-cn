---
title: 用户裁剪平面
description: 用户裁剪平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- 剪辑飞机 WDK Direct3D
- 用户定义的剪辑平面 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f450d693ee1859abe8a6bb56cf3616335aa1c337
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825420"
---
# <a name="user-clip-planes"></a>用户裁剪平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


为最新的 DirectX 版本启用用户定义的剪辑平面。 这些操作与其他剪辑平面的工作方式一样，但它们可由应用程序设置。 驱动程序必须通过响应[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)中的 D3DDP2OP\_SETCLIPPLANE 操作代码来处理这些平面。

 

 





