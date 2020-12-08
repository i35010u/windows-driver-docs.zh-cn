---
title: 在视频捕获驱动程序中通知回调函数
description: 在视频捕获驱动程序中通知回调函数
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw，通知回调函数
- 通知回调函数 WDK 内核模式视频传输
- 回调函数 WDK 内核模式视频传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3eb4e1dd2b74095605c440d84c865a0dfff2111
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830625"
---
# <a name="notify-callback-functions-in-a-video-capture-driver"></a>在视频捕获驱动程序中通知回调函数


## <span id="ddk_notify_callback_functions_in_a_video_capture_driver_gg"></span><span id="DDK_NOTIFY_CALLBACK_FUNCTIONS_IN_A_VIDEO_CAPTURE_DRIVER_GG"></span>


视频捕获驱动程序在视频捕获驱动程序为某些操作调用运行时的 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi) 函数时，为 DirectDraw 运行时提供通知回调函数。 例如，当驱动程序使用 [**DD \_ DxApi \_ OPENVIDEOPORT**](/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))函数标识符调用 **DxApi** 来打开视频端口时，视频捕获驱动程序提供了 [*NotifyCallback*](/windows/win32/api/ddkmapi/nc-ddkmapi-lpdd_notifycallback)函数。 视频端口关闭后，将通知 DirectDraw 运行时，并调用 *NotifyCallback*。 然后，视频捕获驱动程序可以执行与视频端口关闭相关的必要操作。

视频捕获驱动程序在视频捕获驱动程序调用 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)函数并指定以下任意一种函数标识符时，为 DirectDraw 运行时提供 *NotifyCallback* 函数：

-   [**DD \_ DXAPI \_ OPENDIRECTDRAW**](/previous-versions/windows/hardware/drivers/ff550702(v=vs.85))

-   [**DD \_ DXAPI \_ OPENSURFACE**](/previous-versions/windows/hardware/drivers/ff550711(v=vs.85))

-   [**DD \_ DXAPI \_ OPENVIDEOPORT**](/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))

-   [**DD \_ DXAPI \_ 注册 \_ 回调**](/previous-versions/windows/hardware/drivers/ff551502(v=vs.85))

-   [**DD \_ DXAPI \_ OPENVPCAPTUREDEVICE**](/previous-versions/windows/hardware/drivers/ff551500(v=vs.85))

此后，当发生与函数标识符相关联的事件时，DirectDraw 运行时将调用 *NotifyCallback* 函数。 实现视频捕获驱动程序的 *NotifyCallback* ，以执行与事件相关的操作。

 

