---
title: 在视频捕获驱动程序中通知回调函数
description: 在视频捕获驱动程序中通知回调函数
ms.assetid: 2b900436-7874-43a7-97bf-7d1eead78126
keywords:
- DxApi 微型端口驱动程序 WDK DirectDraw，通知回调函数
- 通知回调函数 WDK 内核模式视频传输
- 回调函数 WDK 内核模式视频传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d912fb7b285f0c157eba4a3505dde2e8d484db5b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372805"
---
# <a name="notify-callback-functions-in-a-video-capture-driver"></a>在视频捕获驱动程序中通知回调函数


## <span id="ddk_notify_callback_functions_in_a_video_capture_driver_gg"></span><span id="DDK_NOTIFY_CALLBACK_FUNCTIONS_IN_A_VIDEO_CAPTURE_DRIVER_GG"></span>


视频捕获驱动程序提供时视频捕获驱动程序调用运行时的通知到 DirectDraw 运行时的回调函数[ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi)函数对于某些操作。 例如，视频捕获驱动程序提供，数量[ *NotifyCallback* ](https://docs.microsoft.com/windows/desktop/api/ddkmapi/nc-ddkmapi-lpdd_notifycallback)函数时，驱动程序调用**DxApi**与[ **DD\_DXAPI\_OPENVIDEOPORT** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))函数标识符，若要打开的视频端口。 DirectDraw 运行时的视频端口关闭后，会收到通知，并调用*NotifyCallback*。 视频捕获驱动程序然后可以执行必要的操作相关的视频端口结束。

视频捕获驱动程序提供*NotifyCallback* DirectDraw 运行时视频捕获驱动程序调用的函数[ **DxApi** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxapi/nf-dxapi-dxapi)函数，并指定任何一个以下函数标识符：

-   [**DD\_DXAPI\_OPENDIRECTDRAW**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550702(v=vs.85))

-   [**DD\_DXAPI\_OPENSURFACE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550711(v=vs.85))

-   [**DD\_DXAPI\_OPENVIDEOPORT**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551498(v=vs.85))

-   [**DD\_DXAPI\_REGISTER\_CALLBACK**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551502(v=vs.85))

-   [**DD\_DXAPI\_OPENVPCAPTUREDEVICE**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551500(v=vs.85))

此后，当与函数标识符相关联的事件发生时，DirectDraw 运行时调用*NotifyCallback*函数。 视频捕获驱动程序*NotifyCallback*实现来执行与事件相关的操作。

 

 





