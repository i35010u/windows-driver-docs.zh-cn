---
title: WDM 设备对象的类型
description: WDM 设备对象的类型
ms.assetid: 89cc888d-3097-4637-96d2-6b9c59878d2f
keywords:
- 功能的设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 设备对象 WDK 内核类型
- 筛选器 DOs WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1f8bc429fc7b3b48594dd161e4fc5648216ab6a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382946"
---
# <a name="types-of-wdm-device-objects"></a>WDM 设备对象的类型





有三种类型的 WDM 设备对象：

1.  物理设备对象 (PDO) – 表示到总线上的设备[总线驱动程序](bus-drivers.md)。

2.  功能的设备对象 (FDO) – 表示设备[功能驱动程序](function-drivers.md)。

3.  筛选设备对象 （筛选器执行操作） – 表示设备[筛选器驱动程序](filter-drivers.md)。

三种类型的设备对象是类型的所有[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)，但以不同的方式使用，并且可以具有不同的设备扩展。

驱动程序将自身添加到的设备创建设备对象处理 I/O 的驱动程序堆栈 ([**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)) 并将其附加到设备堆栈 ([ **IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioattachdevicetodevicestack))。 **IoAttachDeviceToDeviceStack**确定当前设备堆栈的顶部，并将新的设备对象附加到设备堆栈的顶部。

 

 




