---
title: 将微型驱动程序绑定到 HID 类
description: 本部分介绍系统提供的 HID 类驱动程序和 HID 微型驱动程序的操作，该操作支持 HIDClass 设备安装程序类中的设备。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97026d721d884113d721857676c26c8f9a9f0dce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791529"
---
# <a name="binding-minidrivers-to-the-hid-class"></a>将微型驱动程序绑定到 HID 类


本部分介绍系统提供的 HID 类驱动程序和 HID 微型驱动程序的操作，该操作支持 HIDClass [设备安装程序类](../install/overview-of-device-setup-classes.md)中的设备。

HID 类驱动程序提供了一个接口，上层驱动程序和用户模式应用程序使用该接口来访问输入设备支持的 HID 集合。 HID 类驱动程序使用 HID 微型驱动程序来访问输入设备的硬件。 HID 微型驱动程序抽象了输入设备连接到的总线端口的操作。 HID 类驱动程序是链接到 HID 微型驱动程序的导出驱动程序。 HID 微型驱动程序通过调用 [**HidRegisterMinidriver**](/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver) 将其操作绑定到 hid 类驱动程序，将其操作绑定到 hid 类驱动程序。

HID 类驱动程序和 HID 微型驱动程序的组合操作充当输入设备的 WDM 函数驱动程序和子设备的总线驱动程序，) 输入设备支持的 (HID 集合。 这种设计使 HID 类驱动程序可以操作连接到端口或总线（而不是 USB 总线）的 USB HID 设备和非 USB 输入设备。 基础父设备的操作细节对于上层驱动程序或用户模式应用程序而言是透明的。

 

