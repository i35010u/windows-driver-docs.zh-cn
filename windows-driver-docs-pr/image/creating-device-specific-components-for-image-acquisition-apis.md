---
title: 为图像采集 API 创建特定于设备的组件
description: 为图像采集 API 创建特定于设备的组件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 561315dfddfb74389d9be440731af82963a470f7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837263"
---
# <a name="creating-device-specific-components-for-image-acquisition-apis"></a>为图像采集 API 创建特定于设备的组件





图像获取 Api （如 TWAIN）通常需要特定于设备的组件，如 TWAIN 数据源。 这些特定于设备的组件应使用 [ISTILLIMAGE Com 接口](istillimage-com-interface.md) 和 [IStiDevice com 接口](istidevice-com-interface.md) 来与用户模式静止映像设备驱动程序和事件监视器进行通信。

图像获取 Api 可以调用 [**IStillImage：： GetDeviceValue**](/previous-versions/windows/hardware/drivers/ff543786(v=vs.85)) 和 [**IStillImage：： SetDeviceValue**](/previous-versions/windows/hardware/drivers/ff543801(v=vs.85)) 来读取和写入 [静止图像设备的注册表项](registry-entries-for-still-image-devices.md)。 例如，每个静止图像设备的 TWAIN 数据源的名称存储在注册表中。

由于 TWAIN API 不允许应用程序在调用数据源时指定活动设备，因此数据源通常会调用 [**IStillImage：： GetDeviceList**](/previous-versions/windows/hardware/drivers/ff543784(v=vs.85)) 以获取所有静止图像设备的列表，然后搜索列表以查找正确的设备，通常基于制造商和型号名称。 制造商和型号文本名称是从安装信息 (INF) 文件中获取的。 因为 TWAIN 对于数据源名称的限制为32个字符，并且因为 WIA 将 "WIA-" 追加到字符串以构造兼容名称，所以 INF 文件中的文本不应超过28个字符。 否则，对整个字符串执行比较（而不仅仅是前32个字符）的 TWAIN 兼容的应用程序可能无法自动找到导致应用程序启动的设备。

若要访问设备，映像获取软件将调用 [**IStillImage：： CreateDevice**](/previous-versions/windows/hardware/drivers/ff543778(v=vs.85)) 以创建定义 **ISTIDEVICE** 接口的 COM 对象的实例。 **IStiDevice** 接口提供了若干用于执行设备 i/o 操作的方法。 创建对象实例时，图像采集软件应指定 "数据" [传输模式](transfer-modes.md)。

映像采集软件可以调用 [**IStiDevice：：订阅**](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe) 来请求事件监视器提供 [静态静止图像设备事件](still-image-device-events.md)的通知。 收到通知后，可以调用 [**IStiDevice：： GetLastNotificationData**](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata) 来确定事件的类型。 [**IStiDevice：：**](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unsubscribe) 不再需要通知时，应调用取消订阅。

当使用 **IStiDevice** 接口完成映像采集软件时，必须调用 [**IStiDevice：： Release**](/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-release)。

 

