---
title: 创建框架设备对象
description: 创建框架设备对象
keywords:
- PnP WDK KMDF，设备对象
- 即插即用 WDK KMDF，设备对象
- 电源管理 WDK KMDF，设备对象
- 设备对象 WDK KMDF
- framework 对象 WDK KMDF，设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20347ad7946f53c3620b18fa81dd3a5d71dea55f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829065"
---
# <a name="creating-a-framework-device-object"></a>创建框架设备对象


每个函数驱动程序、筛选器驱动程序和总线驱动程序都必须为连接到系统的受支持设备的每个实例创建一个框架设备对象。

创建框架设备对象涉及三个步骤：

1.  获取指向 [**WDFDEVICE \_ INIT**](./wdfdevice_init.md) 结构的指针。

    这是一个系统分配的不透明结构，驱动程序将在其中存储有关设备的信息。

2.  正在初始化 WDFDEVICE \_ INIT 结构。

    驱动程序调用一组框架提供的函数，这些函数将信息添加到结构。

3.  调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

    驱动程序将 WDFDEVICE \_ INIT 结构的指针传递到 **WdfDeviceCreate** 方法。 方法创建框架设备对象，并使用 WDFDEVICE INIT 结构中的信息 \_ 来初始化该对象。

有关创建框架设备对象的详细信息，请参阅以下主题：

-   [在功能驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)

-   [在筛选器驱动程序中创建设备对象](creating-device-objects-in-a-filter-driver.md)

-   [在总线驱动程序中创建设备对象](creating-device-objects-in-a-bus-driver.md)

 

