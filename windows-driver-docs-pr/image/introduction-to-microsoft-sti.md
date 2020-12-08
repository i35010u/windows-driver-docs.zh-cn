---
title: Microsoft STI 简介
description: Microsoft STI 简介
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf88e08b923b866c218787f42a773edf04de6633
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828687"
---
# <a name="introduction-to-microsoft-sti"></a>Microsoft STI 简介





Microsoft STI 由以下主要组件构成：

-   [静止图像事件监视器](overview-of-sti-components.md#ddk-still-image-event-monitor-si)，它监视所有已安装的静止图像设备，并在发生[静止图像设备事件](still-image-device-events.md)时接收通知。 事件通常表示设备已准备好传输图像数据。 事件监视器还会跟踪所有已注册的应用程序，并可在检测到事件时启动应用程序。

-   一组由供应商提供的 [用户模式静止图像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si) ，可检测设备活动，并通过静止图像设备事件通知该活动的静止图像事件监视器。 这些微型驱动程序还将内核模式驱动程序中的图像数据传递到上层软件。

-   [扫描仪和照相机控制面板](overview-of-sti-components.md#ddk-scanners-and-cameras-control-panel-si)，允许用户将特定的静止图像设备事件分配给特定的应用程序。 这样，事件监视器将知道在检测到事件时启动哪个应用程序。 控制面板还允许用户测试静止图像设备。

[图像处理应用程序](overview-of-sti-components.md#ddk-imaging-application-si)可将自身注册为 *推送模型感知*，这意味着当静止图像设备准备好传输图像时，事件监视器可以激活该应用程序。

图像处理应用程序通常通过调用高级 [图像采集 API](overview-of-sti-components.md#ddk-image-acquisition-api-si)（如 TWAIN）来读取图像数据流。 映像获取 API 的特定于设备的子组件（如 TWAIN 数据源）使用用户模式静止图像微型驱动程序中的接口执行 i/o 操作。

Microsoft STI 定义了多个 [静止图像 COM 接口](still-image-com-interfaces.md) ，它们允许 STI 组件彼此通信。

下一节将提供有关这些和其他 [MICROSOFT STI 组件](microsoft-sti-components.md)的详细信息。

 

 




