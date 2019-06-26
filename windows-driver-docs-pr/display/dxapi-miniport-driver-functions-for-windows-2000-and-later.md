---
title: Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数
description: Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数
ms.assetid: e9a41e27-930c-49a2-b5e3-0b709b873bb3
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw
- DxApi 微型端口驱动程序 WDK DirectDraw 有关 DxApi 微型端口驱动程序
- autoflipping WDK DirectDraw
- 正在跳过 WDK DirectDraw 字段
- 总线控制 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a442ce47fac9f6414ada2387a1adcbff86efb37c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381069"
---
# <a name="dxapi-miniport-driver-functions-for-windows-2000-and-later"></a>Windows 2000 和更高版本的 DxApi 微型端口驱动程序函数


## <span id="ddk_dxapi_miniport_driver_functions_for_windows_2000_and_later_gg"></span><span id="DDK_DXAPI_MINIPORT_DRIVER_FUNCTIONS_FOR_WINDOWS_2000_AND_LATER_GG"></span>


支持中的 DxApi 界面[微型端口驱动程序](video-miniport-drivers-in-the-windows-2000-display-driver-model.md)仅支持 Windows 2000 和更高版本。

DxApi 接口支持可用于以下操作：

-   使用适用于设备不支持硬件 autoflipping 或具有限制，使其 undependable IRQ Autoflipping。 这允许 DirectDraw 硬件 autoflipping 不可用时始终恢复到软件 autoflipping。

-   正在跳过使用 IRQ 支持 MPEG 驱动程序，可以撤消的 MPEG 数据最初从电影采样 3:2 下拉列表的字段。

-   总线掌握，使设备可以持续将数据传输而无需致电[ *DdLock*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock) / [*DdUnlock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_unlock)为每一帧。 这是特别有用，因为这些设备的驱动程序 WDM 驱动程序。

-   捕获视频并 VBI。 在微型端口驱动程序，它很容易捕获视频的基于硬件的视频端口 IRQ 或图形 IRQ。

 

 





