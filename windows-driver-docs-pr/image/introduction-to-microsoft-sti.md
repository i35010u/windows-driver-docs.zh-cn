---
title: Microsoft STI 简介
description: Microsoft STI 简介
ms.assetid: b329dbbc-28c5-47df-9ced-33180415b7c6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 768ad786bdadeb33ad7640ad629254134c88a54f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358876"
---
# <a name="introduction-to-microsoft-sti"></a>Microsoft STI 简介





Microsoft STI 由以下主要组件组成：

-   一个[静止图像事件监控程序](overview-of-sti-components.md#ddk-still-image-event-monitor-si)，它会监视所有仍安装映像的设备并接收通知时[仍映像设备事件](still-image-device-events.md)发生。 事件通常指示设备已准备好将映像数据传输。 事件监视器还跟踪的所有已注册的应用程序，并检测到事件时，可以启动应用程序。

-   一组的供应商提供[用户模式下仍映像微型驱动程序](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)，可以检测设备活动，并通知该活动通过仍映像设备事件仍映像事件监视器。 这些微型驱动程序还将传递图像数据从内核模式驱动程序到上部级软件。

-   一个[扫描仪和照相机控件面板](overview-of-sti-components.md#ddk-scanners-and-cameras-control-panel-si)，允许用户将特定静止图像设备事件分配给特定的应用程序。 在这种方式，事件监视器将知道哪个应用程序启动时检测到事件。 控制面板还允许用户仍测试映像的设备。

[图像处理应用程序](overview-of-sti-components.md#ddk-imaging-application-si)可以注册其自身作为*推送模型注意*，这意味着它可以通过激活事件监视器时静态图像设备就可以将图像。

图像处理应用程序通常通过调用高级读取映像数据流[图像采集 API](overview-of-sti-components.md#ddk-image-acquisition-api-si)，如 TWAIN。 图像采集 API，如 TWAIN 数据源的特定于设备的子组件为使用到用户模式下仍映像微型驱动程序接口来执行 I/O 操作。

Microsoft STI 定义了多个[仍映像 COM 接口](still-image-com-interfaces.md)允许 STI 组件与彼此进行通信。

下一节提供有关这些和其他详细信息[Microsoft STI 组件](microsoft-sti-components.md)。

 

 




