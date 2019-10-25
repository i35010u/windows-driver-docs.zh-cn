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
ms.openlocfilehash: 420689ea8a01b49329babe95cf1f4ecec34ea7ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836098"
---
# <a name="types-of-wdm-device-objects"></a>WDM 设备对象的类型





有三种 WDM 设备对象：

1.  物理设备对象（PDO）–表示总线[驱动程序与总线驱动程序](bus-drivers.md)的设备。

2.  功能设备对象（FDO）–表示[函数驱动程序](function-drivers.md)的设备。

3.  筛选设备对象（筛选器 DO）–表示[筛选器驱动程序](filter-drivers.md)的设备。

这三种设备对象都是类型[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)，但使用方式不同，可以具有不同的设备扩展。

驱动程序通过创建设备对象（[**IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)）并将其附加到设备堆栈（[**IoAttachDeviceToDeviceStack**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)），将其自身添加到处理设备 i/o 的驱动程序堆栈中。 **IoAttachDeviceToDeviceStack**确定设备堆栈的当前顶部，并将新设备对象附加到设备堆栈的顶部。

 

 




