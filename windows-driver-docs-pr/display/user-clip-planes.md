---
title: 用户裁剪平面
description: 用户裁剪平面
ms.assetid: ea0a7b3b-b850-46bd-b39d-927f28e8de2a
keywords:
- 剪辑平面 WDK Direct3D
- 用户定义的剪辑平面 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbc27498278c10ddee4d32d1930caf5421fc6b5c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389756"
---
# <a name="user-clip-planes"></a>用户裁剪平面


## <span id="ddk_user_clip_planes_gg"></span><span id="DDK_USER_CLIP_PLANES_GG"></span>


用户定义的剪辑平面启用最新版本的 DirectX 版本。 这些工作原理与其他剪辑平面，但它们是可由应用程序设置。 该驱动程序必须处理这些平面回应 D3DDP2OP\_SETCLIPPLANE 操作代码中[ **D3dDrawPrimitives2**](https://msdn.microsoft.com/library/windows/hardware/ff544704)。

 

 





