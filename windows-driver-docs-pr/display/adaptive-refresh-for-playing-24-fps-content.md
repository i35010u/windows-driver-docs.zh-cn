---
title: 用于播放 24 fps 视频内容自适应刷新
description: Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序播放时第二个 (fps) 视频内容每 24 帧 60 Hz 监视器上，它们必须实现 48 Hz 自适应刷新，以节省电量。
ms.assetid: CFA1AE0F-B591-4C5E-A97B-8D4E4B475167
ms.date: 10/19/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: bb0ac9cacd5d61e254dc84f88b1af1a38b401c9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541735"
---
# <a name="adaptive-refresh-for-playing-24-fps-video-content"></a>用于播放 24 fps 视频内容自适应刷新


Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的驱动程序播放时第二个 (fps) 视频内容每 24 帧 60 Hz 监视器上，它们必须实现 48 Hz 自适应刷新，以节省电量。 在此方案中该监视器切换 60 Hz 到 48 Hz 的刷新频率播放 24 fps 视频内容。



## <a name="adaptive-refresh-reference"></a>自适应刷新引用

这些是 WDDM 1.3 和更高版本的驱动程序必须实现为 24 fps 播放的设备驱动程序接口 (DDIs)。

这些参考主题介绍如何在您的驱动程序中实现此功能：

-   [**D3DDDIARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddiarg_checkpresentdurationsupport) 
-   [**DXGI\_DDI\_ARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport) 
-   [**DXGKARG\_SETVIDPNSOURCEADDRESS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddress) (**持续时间**成员)
-   [**DXGKARG\_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay) (**持续时间**成员)
-   [**D3DDDI\_DEVICEFUNCS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) (**pfnCheckPresentDurationSupport**函数指针)
-   [**DXGI1\_3\_DDI\_BASE\_FUNCTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) (**pfnCheckPresentDurationSupport** function pointer)

以下是 Windows 显示驱动程序模型 (WDDM) 1.3 和更高版本的用户模式显示驱动程序的函数必须实现以支持自适应 48 Hz 的刷新频率：

-   [*CheckPresentDurationSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_checkpresentdurationsupport)
-   [*pfnCheckPresentDurationSupport(DXGI)*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport)




 

 





