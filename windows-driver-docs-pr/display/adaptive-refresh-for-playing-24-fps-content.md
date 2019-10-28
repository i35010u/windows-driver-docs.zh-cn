---
title: 进行自适应刷新以播放 24 fps 视频内容
description: 当 Windows 显示器驱动程序模型（WDDM）1.3 及更高版本的驱动程序在 60-Hz 监视器上播放每秒24帧/秒（fps）视频内容时，它们必须实现 48-Hz 自适应刷新以节省电源。
ms.assetid: CFA1AE0F-B591-4C5E-A97B-8D4E4B475167
ms.date: 10/19/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 65c97ff83ae5382c87c84ae2ac6cd9d0798ab791
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839833"
---
# <a name="adaptive-refresh-for-playing-24-fps-video-content"></a>进行自适应刷新以播放 24 fps 视频内容


当 Windows 显示器驱动程序模型（WDDM）1.3 及更高版本的驱动程序在 60-Hz 监视器上播放每秒24帧/秒（fps）视频内容时，它们必须实现 48-Hz 自适应刷新以节省电源。 在此方案中，监视器从 60 Hz 切换到 48-Hz 刷新率以播放 24 fps 视频内容。



## <a name="adaptive-refresh-reference"></a>自适应刷新引用

这些设备驱动程序接口（DDIs）是 WDDM 1.3 和更高版本的驱动程序必须为 24 fps 播放实现的。

以下参考主题介绍如何在驱动程序中实现此功能：

-   [**D3DDDIARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_checkpresentdurationsupport) 
-   [**DXGI\_DDI\_ARG\_CHECKPRESENTDURATIONSUPPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport) 
-   [**DXGKARG\_SETVIDPNSOURCEADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddress) （**Duration**成员）
-   [**DXGKARG\_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay) （**Duration**成员）
-   [**D3DDDI\_DEVICEFUNCS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) （**pfnCheckPresentDurationSupport**函数指针）
-   [**DXGI1\_3\_DDI\_基\_函数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions)（**pfnCheckPresentDurationSupport**函数指针）

下面是 Windows 显示驱动程序模型（WDDM）1.3 和更高版本的用户模式显示驱动程序必须实现的函数，以便支持 48-Hz 自适应刷新速度：

-   [*CheckPresentDurationSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkpresentdurationsupport)
-   [*pfnCheckPresentDurationSupport （DXGI）* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport)




 

 





