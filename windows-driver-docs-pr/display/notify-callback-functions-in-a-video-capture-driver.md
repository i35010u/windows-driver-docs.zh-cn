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
ms.openlocfilehash: f4eff67d8f33f85d044b1540cc09ffc09ae0547e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576158"
---
# <a name="notify-callback-functions-in-a-video-capture-driver"></a>在视频捕获驱动程序中通知回调函数


## <span id="ddk_notify_callback_functions_in_a_video_capture_driver_gg"></span><span id="DDK_NOTIFY_CALLBACK_FUNCTIONS_IN_A_VIDEO_CAPTURE_DRIVER_GG"></span>


视频捕获驱动程序提供时视频捕获驱动程序调用运行时的通知到 DirectDraw 运行时的回调函数[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)函数对于某些操作。 例如，视频捕获驱动程序提供，数量[ *NotifyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff568545)函数时，驱动程序调用**DxApi**与[ **DD\_DXAPI\_OPENVIDEOPORT** ](https://msdn.microsoft.com/library/windows/hardware/ff551498)函数标识符，若要打开的视频端口。 DirectDraw 运行时的视频端口关闭后，会收到通知，并调用*NotifyCallback*。 视频捕获驱动程序然后可以执行必要的操作相关的视频端口结束。

视频捕获驱动程序提供*NotifyCallback* DirectDraw 运行时视频捕获驱动程序调用的函数[ **DxApi** ](https://msdn.microsoft.com/library/windows/hardware/ff557364)函数，并指定任何一个以下函数标识符：

-   [**DD\_DXAPI\_OPENDIRECTDRAW**](https://msdn.microsoft.com/library/windows/hardware/ff550702)

-   [**DD\_DXAPI\_OPENSURFACE**](https://msdn.microsoft.com/library/windows/hardware/ff550711)

-   [**DD\_DXAPI\_OPENVIDEOPORT**](https://msdn.microsoft.com/library/windows/hardware/ff551498)

-   [**DD\_DXAPI\_REGISTER\_CALLBACK**](https://msdn.microsoft.com/library/windows/hardware/ff551502)

-   [**DD\_DXAPI\_OPENVPCAPTUREDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff551500)

此后，当与函数标识符相关联的事件发生时，DirectDraw 运行时调用*NotifyCallback*函数。 视频捕获驱动程序*NotifyCallback*实现来执行与事件相关的操作。

 

 





