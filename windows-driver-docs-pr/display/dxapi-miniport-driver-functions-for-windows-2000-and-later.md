---
title: Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数
description: Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw
- DxApi 微型端口驱动程序 WDK DirectDraw，关于 DxApi 微型端口驱动程序
- autoflipping WDK DirectDraw
- 跳过 WDK DirectDraw 的字段
- 总线控制 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdbe14325e463c864cb3ccf74d623cc1e63b2eb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809087"
---
# <a name="dxapi-miniport-driver-functions-for-windows-2000-and-later"></a>Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数


## <span id="ddk_dxapi_miniport_driver_functions_for_windows_2000_and_later_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_FUNCTIONS_FOR_WINDOWS_2000_AND_LATER_GG"></span>


仅 Windows 2000 和更高版本支持 [视频微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md) 中的 DxApi 接口。

DxApi 接口支持可用于以下操作：

-   Autoflipping 对不支持硬件 Autoflipping 的设备或具有使其 undependable 的限制的设备使用 IRQ。 这允许 DirectDraw 在硬件 autoflipping 不可用时始终还原为软件 autoflipping。

-   字段跳过使用 IRQ 来支持 MPEG 驱动程序，该驱动程序最初从胶片中采样的 MPEG 数据的3:2 下拉。

-   总线主控，因此设备可以持续传输数据而无需为 [*DdLock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)  /  每个帧调用 DdLock [*DdUnlock*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock) 。 这特别有用，因为这些设备的驱动程序是 WDM 驱动程序。

-   捕获视频和 VBI。 在微型端口驱动程序中，可以轻松捕获基于硬件视频端口 IRQ 或图形 IRQ 的视频。

 

