---
title: 驱动程序管理的资源
description: 驱动程序管理的资源
ms.assetid: f68b622a-247a-4a89-8d4c-c6a306b7fb3e
keywords:
- 纹理管理 WDK Direct3D，驱动程序管理的资源
- 驱动程序管理的资源 WDK Direct3D
- 可管理的资源 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02ab4c28fd86ab1c1c70b5da42a4d7a3dc317cd7
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066735"
---
# <a name="driver-managed-resources"></a>驱动程序管理的资源


## <span id="ddk_driver_managed_resources_gg"></span><span id="DDK_DRIVER_MANAGED_RESOURCES_GG"></span>


除了支持 [由驱动程序管理的纹理](driver-managed-textures.md)中所述的纹理管理，DirectX 8.1 驱动程序还可以管理一般的资源，如纹理、音量纹理、立方体地图纹理、顶点缓冲区和索引缓冲区。

驱动程序通过将[**DDCORECAPS**](/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**dwCaps2**成员设置为 DDCAPS2 CANMANAGERESOURCE 位，来支持驱动程序托管的资源 \_ 。 驱动程序在[**DD \_ HALINFO**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构的**ddCaps**成员中指定此 DDCORECAPS 结构。 DD \_ HALINFO 由 [**DrvGetDirectDrawInfo**](/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo) 返回，以响应驱动程序的 DirectDraw 组件的初始化。

 

