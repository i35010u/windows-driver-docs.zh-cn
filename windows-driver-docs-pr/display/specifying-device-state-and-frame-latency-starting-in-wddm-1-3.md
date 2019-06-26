---
title: 在 WDDM 1.3 中指定设备状态和帧延迟
ms.assetid: 97FC54BD-0D20-4235-B914-5F44690274AE
description: 从在 Windows 显示驱动程序模型 (WDDM) 1.3，用户模式显示驱动程序可以使用转义标志将传递给显示微型端口驱动程序的设备状态和帧延迟信息。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 937114aca5fe1017617e4e36c4659837945fd28c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376071"
---
# <a name="specifying-device-state-and-frame-latency-in-wddm-13"></a>在 WDDM 1.3 中指定设备状态和帧延迟


从在 Windows 显示驱动程序模型 (WDDM) 1.3，用户模式显示驱动程序可以使用转义标志传递到显示微型端口驱动程序的设备状态和帧延迟信息时[ *pfnEscapeCb* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb)调用函数。 可以在使用这些标记[ **D3DDDI\_ESCAPEFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags)结构在 Windows 8.1 中启动。

这些参考主题介绍如何在用户模式显示驱动程序中实现此功能：

-   [**D3DDDI\_DEVICEEXECUTION\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddi_deviceexecution_state)
-   [**D3DDDI\_EXECUTIONSTATEESCAPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_executionstateescape)
-   [**D3DDDI\_FRAMELATENCYESCAPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_framelatencyescape)
-   [**D3DDDI\_ESCAPEFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags) (新**DeviceStatusQuery**并**ChangeFrameLatency**成员)

 

 





