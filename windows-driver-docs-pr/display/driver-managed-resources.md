---
title: 驱动程序管理的资源
description: 驱动程序管理的资源
ms.assetid: f68b622a-247a-4a89-8d4c-c6a306b7fb3e
keywords:
- 纹理管理 WDK Direct3D，驱动程序管理资源
- 驱动程序管理资源 WDK Direct3D
- 可管理资源 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68e935462ea876a3c11ee2bc4b4a747d7bdf1c4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353850"
---
# <a name="driver-managed-resources"></a>驱动程序管理的资源


## <span id="ddk_driver_managed_resources_gg"></span><span id="DDK_DRIVER_MANAGED_RESOURCES_GG"></span>


除了支持纹理管理，如中所述[Driver-Managed 纹理](driver-managed-textures.md)，DirectX 8.1 驱动程序还可以管理资源一般情况下，如纹理、 体积纹理、 立方体贴图纹理、 顶点缓冲区和索引缓冲区。

该驱动程序支持通过设置驱动程序管理资源**dwCaps2**的成员[ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构 DDCAPS2\_CANMANAGERESOURCE 位. 该驱动程序指定在此 DDCORECAPS 结构**ddCaps**的成员[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构。 DD\_返回 HALINFO [ **DrvGetDirectDrawInfo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)响应 DirectDraw 组件的驱动程序的初始化。

 

 





