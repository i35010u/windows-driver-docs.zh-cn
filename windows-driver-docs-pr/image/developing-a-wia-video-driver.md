---
title: 开发 WIA 视频驱动程序
description: 开发 WIA 视频驱动程序
ms.assetid: 3cf14fd3-1dfa-480e-a69c-c4d2c196a504
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d70cdd87a61c49c7cdf2cdb04876c48b5c22456b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189619"
---
# <a name="developing-a-wia-video-driver"></a>开发 WIA 视频驱动程序





WIA 支持视频和视频相机。 要使用 WIA 的视频摄像机应使用 Windows Me、Windows XP 和更高版本的操作系统版本随附的视频驱动程序，或者开发 DirectShow 视频驱动程序。 WIA 依赖于 DirectShow 从视频流获取静止图像。

WIA 仅需对 DirectShow 驱动程序的 INF 文件进行少量修改，WIA 才能将其识别为受支持的相机。 必要的更改包括：

```INF
[Device]
Include= sti.inf
Needs= STI.WIAVideo.Registration
SubClass=StillImage
DeviceType=3
DeviceSubType=0x1
Capabilities=0x00000031
ICMProfiles="sRGB Color Space Profile.icm"
```

如果未进行这些添加，WIA 将无法识别设备。 请确保将这些更改 *添加* 到您的 INF 文件。 不要将 INF 文件替换为以下行。

有关如何使用 USBCAMD 模型通过视频相机支持 WIA 的示例，请参阅 [带有捕获按钮的基于 USB 的相机](../stream/usb-based-camera-with-a-capture-button.md)。

 

