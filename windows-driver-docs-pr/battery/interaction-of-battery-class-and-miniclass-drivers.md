---
title: 电池类和微型类驱动程序的交互
description: 电池类和微型类驱动程序的交互
ms.assetid: bf35a034-1bb9-4106-aafe-7692d0ff92d0
keywords:
- 电池 miniclass 驱动程序 WDK，电池类驱动程序交互
- 电池类驱动程序 WDK，电池 miniclass 驱动程序交互
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e66ae9502d314715d099a6dd929a3d6cd7bb13d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335265"
---
# <a name="interaction-of-battery-class-and-miniclass-drivers"></a>电池类和微型类驱动程序的交互


## <span id="ddk_interaction_of_battery_class_and_miniclass_drivers_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_CLASS_AND_MINICLASS_DRIVERS_DG"></span>


在一起，电池类驱动程序和 miniclass 驱动程序管理的计算机使用电池。 下图显示了这些两个驱动程序的交互方式。

![说明电池类和 miniclass 驱动程序的交互的关系图](images/battmini.png)

Miniclass 驱动程序是它控制的设备的主要功能驱动程序。 从电源管理器通过复合电池驱动程序接收 Irp，调用在电池类驱动程序以便注册其设备，以报告状态，并处理某些系统定义的电池电量 Ioctl 支持例程。

类驱动程序接收来自所有 miniclass 驱动程序的信息和状态，并报告给电源管理器通过复合电池驱动程序。 在响应电池 Ioctl，类驱动程序调用[电池 miniclass 驱动程序例程](https://msdn.microsoft.com/library/windows/hardware/ff536286)(BatteryMini*Xxx*例程) 中执行特定的设备管理操作的 miniclass 驱动程序。 此外，可以发送应用程序，如电表[ **IRP\_MJ\_设备\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff550744) miniclass 驱动程序的请求，若要获取其相关信息特定的电池。

在类驱动程序设计为处理可能出现的电池信息和条件，包括温度，容量，等等; 中的更改的超集单个电池的功能检测并报告所有这些情况会有所不同。 每个 miniclass 驱动程序应设计为可管理其特定电池类型，必须正确响应类驱动程序时需要电池不支持任何信息。

 

 




