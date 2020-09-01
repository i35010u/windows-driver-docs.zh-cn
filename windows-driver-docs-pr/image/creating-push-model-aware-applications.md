---
title: 创建推送模型感知应用程序
description: 创建推送模型感知应用程序
ms.assetid: 0f554b2c-0217-4109-8ef6-99c5400dfed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 507c3a07a105ea8ad7206b7e5cede7780dd4025a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191713"
---
# <a name="creating-push-model-aware-applications"></a>创建推送模型感知应用程序





推送模型识别应用程序是指向 Microsoft STI 注册了自己的应用程序，以便在发生静止图像设备事件时可以自动激活它。 可以通过以下两种方法之一来使应用程序能够识别推送模型：

-   调用 [**IStillImage：： RegisterLaunchApplication**](/previous-versions/windows/hardware/drivers/ff543798(v=vs.85))。 应用程序或其安装程序可以进行调用。

-   在应用程序的安装信息 (INF) 文件中包含一项。 INF 文件中的 [**Inf AddReg 指令**](../install/inf-addreg-directive.md) 应引用该条目。 下面的示例演示了该项的语法：

    ```INF
    ; Register Application "Imaging" as a push-model aware application for use with the still image event monitor
    HKLM,"SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered Applications",Imaging,,"%25%\KodakImg.Exe /StiDevice:%%1 /StiEvent:%%2"
    ```

    支持推送模型识别应用程序的设备需要两个 INF 文件条目： **DeviceData** 和 **事件**。 有关详细信息，请参阅 [适用于静止图像设备的 INF 文件](inf-files-for-still-image-devices.md)。

其中的任何一种方法都会导致应用程序注册到 " [静态映像" 事件监视器](overview-of-sti-components.md#ddk-still-image-event-monitor-si)。

如果将应用程序注册为推送模型感知，用户可以使用扫描仪和照相机控制面板将 [静止图像设备事件](still-image-device-events.md) 分配给应用程序。 此外，供应商可以通过在设备驱动程序的 INF 文件中包含应用程序名称来向应用程序提供设备事件的初始分配。 用户可以使用扫描仪和照相机控制面板更改此初始分配。

将设备事件分配给应用程序后，事件监视器将在检测到已分配的设备事件发生时启动该应用程序。

当激活推送模型感知应用程序时，它应调用 [**IStillImage：： GetSTILaunchInformation**](/previous-versions/windows/hardware/drivers/ff543790(v=vs.85)) 来确定事件以及启动该应用程序的设备。 然后，它可以调用 [**IStillImage：： GetDeviceInfo**](/previous-versions/windows/hardware/drivers/ff543782(v=vs.85)) 以获取有关设备的详细信息。

应用程序必须处理该事件，或者必须创建一个用户显示，说明为什么无法处理该事件。 因此，用户将使用 "控制面板" 将设备事件与其他某个应用程序相关联。

处理事件通常表示在图像中进行读取。 为此，应用程序通常会调用 [图像获取 API](overview-of-sti-components.md#ddk-image-acquisition-api-si)，如 TWAIN。

如果应用程序已启动，因为发生了某个事件，但图像获取 API 在数据模式下未打开该设备 (请参阅 [传输模式](transfer-modes.md)) ，如果检测到其他事件，事件监视器将启动该应用程序的另一个实例。 必须实现应用程序，以便它允许多个实例或 (最好地) 识别不是第一个实例时，将消息发送到标识事件的第一个实例，然后退出。

 

