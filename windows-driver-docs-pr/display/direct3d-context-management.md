---
title: Direct3D 上下文管理
description: Direct3D 上下文管理
ms.assetid: 143f5150-9ac4-43f7-985f-0baa32871af2
keywords:
- 上下文 WDK Direct3D
- Direct3D WDK Windows 2000 显示，上下文管理
- 有关上下文管理上下文 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c8e07b466c989b1dbcc4ef966b0be70b6532f1a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342399"
---
# <a name="direct3d-context-management"></a>Direct3D 上下文管理


## <span id="ddk_direct3d_context_management_gg"></span><span id="DDK_DIRECT3D_CONTEXT_MANAGEMENT_GG"></span>


上下文封装应用程序创建 Microsoft Direct3D 硬件抽象层 (HAL) 的设备; 的状态信息也就是说，上下文描述该驱动程序应如何绘制。 状态包括呈现到的图面、 深度图面，明暗度信息和纹理信息等信息。

Direct3D 驱动程序负责创建和管理其自己的呈现上下文。

 

 





