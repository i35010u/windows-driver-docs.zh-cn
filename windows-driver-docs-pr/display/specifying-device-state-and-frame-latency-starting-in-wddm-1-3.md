---
title: 在 WDDM 1.3 中指定设备状态和帧延迟
ms.assetid: 97FC54BD-0D20-4235-B914-5F44690274AE
description: 从在 Windows 显示驱动程序模型 (WDDM) 1.3，用户模式显示驱动程序可以使用转义标志将传递给显示微型端口驱动程序的设备状态和帧延迟信息。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 3254cb07f8e14b3dd70006b0e8b071eec6256520
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389979"
---
# <a name="specifying-device-state-and-frame-latency-in-wddm-13"></a>在 WDDM 1.3 中指定设备状态和帧延迟


从在 Windows 显示驱动程序模型 (WDDM) 1.3，用户模式显示驱动程序可以使用转义标志传递到显示微型端口驱动程序的设备状态和帧延迟信息时[ *pfnEscapeCb* ](https://msdn.microsoft.com/library/windows/hardware/ff568908)调用函数。 可以在使用这些标记[ **D3DDDI\_ESCAPEFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544541)结构在 Windows 8.1 中启动。

这些参考主题介绍如何在用户模式显示驱动程序中实现此功能：

-   [**D3DDDI\_DEVICEEXECUTION\_状态**](https://msdn.microsoft.com/library/windows/hardware/dn482416)
-   [**D3DDDI\_EXECUTIONSTATEESCAPE**](https://msdn.microsoft.com/library/windows/hardware/dn482417)
-   [**D3DDDI\_FRAMELATENCYESCAPE**](https://msdn.microsoft.com/library/windows/hardware/dn482418)
-   [**D3DDDI\_ESCAPEFLAGS** ](https://msdn.microsoft.com/library/windows/hardware/ff544541) (新**DeviceStatusQuery**并**ChangeFrameLatency**成员)

 

 





