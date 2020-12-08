---
title: 在 WDDM 1.3 中指定设备状态和帧延迟
description: 从 Windows 显示器驱动程序模型 (WDDM) 1.3 开始，用户模式显示驱动程序可以使用转义标志将设备状态和帧延迟信息传递到显示微型端口驱动程序。
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 05d158539f44ef95380f56cd115d0fda4d66454a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815443"
---
# <a name="specifying-device-state-and-frame-latency-in-wddm-13"></a>在 WDDM 1.3 中指定设备状态和帧延迟


从 Windows 显示器驱动程序模型 (WDDM) 1.3 开始，在调用 [*pfnEscapeCb*](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_escapecb) 函数时，用户模式显示驱动程序可以使用转义标志将设备状态和帧延迟信息传递到显示微型端口驱动程序。 从 Windows 8.1 开始的 [**D3DDDI \_ ESCAPEFLAGS**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags) 结构中提供了这些标志。

以下参考主题介绍如何在用户模式显示驱动程序中实现此功能：

-   [**D3DDDI \_ DEVICEEXECUTION \_ 状态**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddi_deviceexecution_state)
-   [**D3DDDI \_ EXECUTIONSTATEESCAPE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_executionstateescape)
-   [**D3DDDI \_ FRAMELATENCYESCAPE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddi_framelatencyescape)
-   [**D3DDDI \_ESCAPEFLAGS**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_escapeflags) (New **DeviceStatusQuery** 和 **ChangeFrameLatency** 成员) 

 

