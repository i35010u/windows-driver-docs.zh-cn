---
title: Direct3D 上下文管理
description: Direct3D 上下文管理
keywords:
- 上下文 WDK Direct3D
- Direct3D WDK Windows 2000 显示，上下文管理
- 上下文 WDK Direct3D，关于上下文管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc5ac84a3d1fc6dc48f8069eaffe5370b94d1484
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809483"
---
# <a name="direct3d-context-management"></a>Direct3D 上下文管理


## <span id="ddk_direct3d_context_management_gg"></span><span id="DDK_DIRECT3D_CONTEXT_MANAGEMENT_GG"></span>


上下文封装了应用程序创建的 Microsoft Direct3D 硬件抽象层 (HAL) 设备的状态信息;也就是说，上下文描述了驱动程序的绘制方式。 状态包括呈现到的图面、深度图面、阴影信息和纹理信息等信息。

Direct3D 驱动程序负责创建和管理其自己的呈现上下文。

 

 





