---
title: WDM 设备对象的类型
description: WDM 设备对象的类型
ms.assetid: 89cc888d-3097-4637-96d2-6b9c59878d2f
keywords:
- 功能设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 设备对象 WDK 内核，类型
- 筛选 DOs WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6c86b7f56031335be9abf429c03b3ad7db6cbfc
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185605"
---
# <a name="types-of-wdm-device-objects"></a>WDM 设备对象的类型





有三种 WDM 设备对象：

1.   (PDO) 的物理设备对象–表示总线 [驱动程序](bus-drivers.md)的总线上的设备。

2.  功能设备对象 (FDO) –表示 [功能驱动程序](function-drivers.md)的设备。

3.  筛选设备对象 (filter DO) –表示设备到 [筛选器驱动程序](filter-drivers.md)。

这三种设备对象均为类型 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)，但使用方式不同，并且可以具有不同的设备扩展。

驱动程序通过创建 ([**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)) 的设备对象并将其附加到设备堆栈 ([**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)) ，将自身添加到处理设备 i/o 的驱动程序堆栈中。 **IoAttachDeviceToDeviceStack** 确定设备堆栈的当前顶部，并将新设备对象附加到设备堆栈的顶部。

 

