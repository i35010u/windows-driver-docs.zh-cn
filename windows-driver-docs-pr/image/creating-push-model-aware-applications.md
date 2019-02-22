---
title: 创建推送模型识别应用程序
description: 创建推送模型识别应用程序
ms.assetid: 0f554b2c-0217-4109-8ef6-99c5400dfed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f80031cc9d7a1f132dbdcd854dedfe30e142a43
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541042"
---
# <a name="creating-push-model-aware-applications"></a>创建推送模型识别应用程序





推送模型感知应用程序是指注册其自身的 Microsoft STI，以便它可以自动激活静止图像设备事件发生时。 应用程序可以进行推送模型注意通过以下两种方法之一：

-   调用[ **IStillImage::RegisterLaunchApplication**](https://msdn.microsoft.com/library/windows/hardware/ff543798)。 由应用程序或通过其安装程序，可以进行调用。

-   在应用程序的安装信息 (INF) 文件中包括一个条目。 应通过引用的项[ **INF AddReg 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546320) INF 文件中。 下面的示例说明了项的语法：

    ```INF
    ; Register Application "Imaging" as a push-model aware application for use with the still image event monitor
    HKLM,"SOFTWARE\Microsoft\Windows\CurrentVersion\StillImage\Registered Applications",Imaging,,"%25%\KodakImg.Exe /StiDevice:%%1 /StiEvent:%%2"
    ```

    两个 INF 文件条目所需的支持推送模型识别应用程序的设备：**DeviceData**并**事件**。 有关详细信息，请参阅[静止图像设备 INF 文件](inf-files-for-still-image-devices.md)。

其中一种方法会导致应用程序能够注册到[静止图像事件监控程序](overview-of-sti-components.md#ddk-still-image-event-monitor-si)。

如果应用程序注册为注意推送模型，用户可以分配[仍映像设备事件](still-image-device-events.md)到应用程序使用的扫描仪和照相机控件面板。 此外，供应商可以提供对应用程序的设备事件的初始分配包括设备驱动程序的 INF 文件中的应用程序名称。 用户可以更改此初始分配使用扫描仪和照相机控件面板。

设备事件已分配给应用程序后，事件监视器将检测到分配的设备事件发生时启动应用程序。

推送模型感知应用程序激活时，它应调用[ **IStillImage::GetSTILaunchInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff543790)来确定事件，并为其启动的设备。 然后，它可以调用[ **IStillImage::GetDeviceInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff543782)以获取有关设备的详细信息。

应用程序必须处理该事件，或它必须创建解释为什么它无法处理该事件的用户显示。 有可能用户然后将使用控制面板以将设备事件与其他一些应用程序相关联。

处理事件通常意味着在图像中的读取。 若要执行此操作，该应用程序通常会调用[图像采集 API](overview-of-sti-components.md#ddk-image-acquisition-api-si)，如 TWAIN。

如果因为发生了事件，但图像采集 API 没有在数据模式中打开设备启动的应用程序 (请参阅[传输模式](transfer-modes.md))，如果另一个事件，事件监视器将启动应用程序的另一个实例检测到。 必须实现应用程序，以便允许多个实例或 （最好） 识别时它不是第一个实例，将消息发送到第一个实例标识事件，并退出。

 

 




