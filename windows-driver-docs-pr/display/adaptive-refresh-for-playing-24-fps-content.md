---
title: 进行自适应刷新以播放 24 fps 视频内容
description: 当 Windows 显示器驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序每秒播放24帧， (60-Hz 监视器上的 fps) 视频内容时，它们必须实现 48-Hz 自适应刷新才能节省电源。
ms.assetid: CFA1AE0F-B591-4C5E-A97B-8D4E4B475167
ms.date: 10/19/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: f0527453e4d1b29e1f718d40848e786bdb07164c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063190"
---
# <a name="adaptive-refresh-for-playing-24-fps-video-content"></a>进行自适应刷新以播放 24 fps 视频内容


当 Windows 显示器驱动程序模型 (WDDM) 1.3 及更高版本的驱动程序每秒播放24帧， (60-Hz 监视器上的 fps) 视频内容时，它们必须实现 48-Hz 自适应刷新才能节省电源。 在此方案中，监视器从 60 Hz 切换到 48-Hz 刷新率以播放 24 fps 视频内容。



## <a name="adaptive-refresh-reference"></a>自适应刷新引用

它们是 (DDIs) 的设备驱动程序接口，而 WDDM 1.3 和更高版本的驱动程序必须为 24 fps 播放实现此功能。

以下参考主题介绍如何在驱动程序中实现此功能：

-   [**D3DDDIARG \_ CHECKPRESENTDURATIONSUPPORT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddiarg_checkpresentdurationsupport) 
-   [**DXGI \_ DDI \_ ARG \_ CHECKPRESENTDURATIONSUPPORT**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport) 
-   [**DXGKARG \_SETVIDPNSOURCEADDRESS**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddress) (**Duration** 成员) 
-   [**DXGKARG \_SETVIDPNSOURCEADDRESSWITHMULTIPLANEOVERLAY**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_setvidpnsourceaddresswithmultiplaneoverlay) (**Duration** 成员) 
-   [**D3DDDI \_DEVICEFUNCS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_devicefuncs) (**pfnCheckPresentDurationSupport** 函数指针) 
-   [**DXGI1 \_ 3 \_ DDI \_ 基本 \_ 函数**](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi1_3_ddi_base_functions) (**pfnCheckPresentDurationSupport** 函数指针) 

下面是 Windows 显示器驱动程序模型 (WDDM) 1.3 和更高版本的用户模式显示驱动程序必须实现的函数，以便支持 48-Hz 自适应刷新率：

-   [*CheckPresentDurationSupport*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_checkpresentdurationsupport)
-   [*pfnCheckPresentDurationSupport (DXGI) *](/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-_dxgi_ddi_arg_checkpresentdurationsupport)




 

