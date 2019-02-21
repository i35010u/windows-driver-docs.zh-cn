---
title: 创建框架设备对象
description: 创建框架设备对象
ms.assetid: 25023c19-a153-4bd4-9fb6-3a1bf85860aa
keywords:
- 即插即用 WDK KMDF，设备对象
- 插 WDK KMDF，设备对象
- 电源管理 WDK KMDF，设备对象
- 设备对象 WDK KMDF
- framework 对象 WDK KMDF，设备对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f94a1a8a2989fb80d3f497eb0613974ab32928ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547676"
---
# <a name="creating-a-framework-device-object"></a>创建框架设备对象


每个功能驱动程序、 筛选器驱动程序和总线驱动程序必须创建的受支持的设备连接到系统的每个实例是 framework 的设备对象。

创建框架设备对象涉及三个步骤：

1.  获取一个指向[ **WDFDEVICE\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff546951)结构。

    这是不透明，将为系统分配的结构，该驱动程序在其中存储有关设备的信息。

2.  初始化 WDFDEVICE\_INIT 结构。

    该驱动程序调用一系列将信息添加到结构的框架提供的函数。

3.  调用[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)。

    驱动程序通过 WDFDEVICE\_INIT 结构的指针，指向**WdfDeviceCreate**方法。 此方法创建 framework 设备对象并使用 WDFDEVICE 中的信息\_INIT 结构来初始化对象。

有关创建设备对象的框架的详细信息，请参阅以下主题：

-   [在功能驱动程序中创建设备对象](creating-device-objects-in-a-function-driver.md)

-   [在筛选器驱动程序中创建设备对象](creating-device-objects-in-a-filter-driver.md)

-   [在总线驱动程序中创建设备对象](creating-device-objects-in-a-bus-driver.md)

 

 





