---
title: 生成 MIP 贴图纹理的子级别
description: 生成 MIP 贴图纹理的子级别
keywords:
- MIP map 纹理 WDK DirectX 9.0，生成子级别
- MIP 地图9.0 纹理的子层
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b20d2ffccba63cfc91d8cb920e43c9d3b29a780e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803905"
---
# <a name="generating-sublevels-of-mip-map-textures"></a>生成 MIP 贴图纹理的子级别


## <span id="ddk_generating_sublevels_of_mip_map_textures_gg"></span><span id="DDK_GENERATING_SUBLEVELS_OF_MIP_MAP_TEXTURES_GG"></span>


显示驱动程序指示支持通过设置 \_ [**DDCORECAPS**](/windows/win32/api/ddrawi/ns-ddrawi-ddcorecaps)结构的 **dwCaps2** 成员的 DDCAPS2 CANAUTOGENMIPMAP 位来自动生成 MIP 地图纹理的子级别。 驱动程序在 [**DD \_ HALINFO**](/windows/win32/api/ddrawint/ns-ddrawint-dd_halinfo)结构的 **ddCaps** 成员中指定此 DDCORECAPS 结构。 DD \_ HALINFO 由驱动程序的 [**DrvGetDirectDrawInfo**](/windows/win32/api/winddi/nf-winddi-drvgetdirectdrawinfo) 函数返回。 显示驱动程序还指示特定的 surface 格式是否支持通过 \_ \_ 在格式的 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **dwOperations** 成员中设置 D3DFORMAT OP AUTOGENMIPMAP 标志来自动生成子层。

创建纹理图面时，Direct3D 运行时将 \_ DDSCAPSEX ([**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))) 结构的 **dwCaps3** 成员的 DDSCAPS3 AUTOGENMIPMAP 位设置为，以指示可以自动生成此纹理的 MIP 映射子级别。 如果 Direct3D 指示某些纹理自动生成其 MIP 地图子级别，而某些纹理未自动生成，则驱动程序只能对这些纹理 (D3DDP2OP TEXBLT) 执行 array.blit 操作， \_ 如以下方案所述：

-   驱动程序无法从自动生成 MIP 映射的源纹理 array.blit 到不会生成的目标纹理。

-   如果驱动程序从不自动生成 MIP 映射的源纹理 blits，则该驱动程序仅 blits 最顶层的匹配级别。 将忽略源纹理的子级别。 可以生成目标子级别。

-   同样，如果驱动程序 blits 从源到目标的纹理，这两种类型都自动生成 MIP maps，则驱动程序仅 blits 最顶层的匹配级别。 将忽略源纹理的子级别。 可以生成目标子级别。

为了生成 MIP 地图纹理的子级别，驱动程序将接收 D3DDP2OP \_ GENERATEMIPSUBLEVELS 命令和 [**D3DHAL \_ DP2GENERATEMIPSUBLEVELS**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2generatemipsublevels) 结构。 为了接收此命令，纹理的表面格式必须公开 D3DFORMAT \_ OP \_ AUTOGENMIPMAP 标志。

对于 [驱动程序管理的资源](driver-managed-resources.md)，当驱动程序逐出并替换视频内存中的资源时，驱动程序必须使用最后一次设置的筛选器类型来自动生成子级别。 因为 Direct3D 不控制资源的逐出和替换，所以 Direct3D 不会将 D3DDP2OP \_ GENERATEMIPSUBLEVELS 命令发送到驱动程序。

Direct3D 运行时无法调用驱动程序的 [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) 函数，也无法使用任何其他 [DDI](direct3d-driver-ddi.md) 来访问自动生成的 MIP 地图纹理的子级别。 这意味着，自动生成的 MIP 地图纹理的子级别（如轻型 MIP 地图纹理）是 "隐式的"，可根据需要由驱动程序指定。 驱动程序无需指定 "complete" 表面数据结构。 但请注意，Direct3D 必须能够调用驱动程序的 *DdLock* 或 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 函数，发送 D3DDP2OP \_ BLT 命令，或使用任何其他 DDI (来查找 [驱动程序管理的纹理](driver-managed-textures.md)、动态纹理或供应商特定格式仅) 访问自动生成的 MIP 地图纹理的顶层。

 

