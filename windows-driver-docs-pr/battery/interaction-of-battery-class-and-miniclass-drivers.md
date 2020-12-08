---
title: 电池类和微型类驱动程序的交互
description: 电池类和微型类驱动程序的交互
keywords:
- 电池 miniclass 驱动程序 WDK，电池类驱动程序交互
- 电池类驱动程序 WDK，电池 miniclass 驱动程序交互
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ec8306e2086764ab8f3b946b7f9d6684c4e7478
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798681"
---
# <a name="interaction-of-battery-class-and-miniclass-drivers"></a>电池类和微型类驱动程序的交互


## <span id="ddk_interaction_of_battery_class_and_miniclass_drivers_dg"></span><span id="DDK_INTERACTION_OF_BATTERY_CLASS_AND_MINICLASS_DRIVERS_DG"></span>


同时，电池类驱动程序和 miniclass 驱动程序管理计算机的电池使用情况。 下图显示了这两个驱动程序的交互方式。

![说明电池类和 miniclass 驱动程序的交互的关系图](images/battmini.png)

Miniclass 驱动程序是它控制的设备的主要功能驱动程序。 它通过复合电池驱动程序从电源管理器接收 Irp，并调用电池类驱动程序中的支持例程来注册其设备、报告状态并处理某些系统定义的电池 IOCTLs。

类驱动程序接收所有 miniclass 驱动程序的信息和状态，并通过复合电池驱动程序将其报告给电源管理器。 为了响应电池 IOCTLs，类驱动程序在 miniclass 驱动程序中调用 [电池 miniclass 驱动程序](/windows-hardware/drivers/ddi/_battery/)*)  (* 例程以执行特定设备控制操作。 此外，应用程序（如电源指示器）可以将 [**IRP \_ MJ \_ 设备 \_ 控制**](../kernel/irp-mj-device-control.md) 请求发送到 miniclass 驱动程序，以获取有关特定电池的信息。

类驱动程序设计用于处理可能的电池信息和条件的超集，包括温度、容量变化等等;单个电池的检测和报告这些条件的能力有所不同。 每个 miniclass 驱动程序都应该设计为管理其特定电池类型，并在要求提供电池不支持的任何信息时，正确响应类驱动程序。

 

