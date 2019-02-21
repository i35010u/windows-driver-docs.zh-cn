---
title: 为图像采集 Api 创建特定于设备的组件
description: 为图像采集 Api 创建特定于设备的组件
ms.assetid: c4906dec-6d34-47f5-abde-0513c4499a66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 427b873b8a1ea84a1154e1eb5aef8ed44d72f13d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522901"
---
# <a name="creating-device-specific-components-for-image-acquisition-apis"></a>为图像采集 Api 创建特定于设备的组件





图像采集 Api，如 TWAIN，通常需要特定于设备的组件，如 TWAIN 数据源。 应使用这些特定于设备的组件[IStillImage COM 接口](istillimage-com-interface.md)并[IStiDevice COM 接口](istidevice-com-interface.md)与用户模式下仍映像设备驱动程序和事件监视程序进行通信。

图像 Api 可以调用的采集[ **IStillImage::GetDeviceValue** ](https://msdn.microsoft.com/library/windows/hardware/ff543786)并[ **IStillImage::SetDeviceValue** ](https://msdn.microsoft.com/library/windows/hardware/ff543801)读取和写入[注册表项静止图像设备](registry-entries-for-still-image-devices.md)。 例如，在注册表中存储每个静态图像设备 TWAIN 数据源的名称。

TWAIN API 不允许的应用程序来调用数据源时指定的活动设备，因为数据源通常会调用[ **IStillImage::GetDeviceList** ](https://msdn.microsoft.com/library/windows/hardware/ff543784)来获取所有仍列表图像设备，并将搜索列表以查找正确的设备，通常按制造商和型号名称。 从安装程序信息 (INF) 文件获取制造商和型号的文本名称。 因为 TWAIN 有 32 个字符限制的数据源名称和 WIA 将追加"WIA-"到字符串构造兼容的名称，因为 INF 文件中的文本应不能超过 28 个字符。 否则为 TWAIN 兼容的应用程序的整个字符串，并不只是前 32 个字符，在执行比较可能无法再以自动查找导致启动的应用程序的设备。

若要访问的设备，图像获取软件调用[ **IStillImage::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff543778)若要创建定义的 COM 对象的实例**IStiDevice**接口。 **IStiDevice**接口提供了几种方法执行设备 I/O 操作。 图像获取软件创建对象实例时，应指定"数据"[传输模式](transfer-modes.md)。

可以调用图像获取软件[ **IStiDevice::Subscribe** ](https://msdn.microsoft.com/library/windows/hardware/ff543768)请求事件监视器的通知传递[仍映像设备事件](still-image-device-events.md)。 一旦收到通知时， [ **IStiDevice::GetLastNotificationData** ](https://msdn.microsoft.com/library/windows/hardware/ff543751)可以调用以确定事件类型。 [**IStiDevice::UnSubscribe** ](https://msdn.microsoft.com/library/windows/hardware/ff543773)不再需要通知时，应调用。

当图像获取软件使用完**IStiDevice**接口，它必须调用[ **IStiDevice::Release**](https://msdn.microsoft.com/library/windows/hardware/ff543765)。

 

 




