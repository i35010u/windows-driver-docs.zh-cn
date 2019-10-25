---
title: 将微型驱动程序绑定到 HID 类
description: 本部分介绍系统提供的 HID 类驱动程序和 HID 微型驱动程序的操作，该操作支持 HIDClass 设备安装程序类中的设备。
ms.assetid: 2B51E205-8EBB-413A-A317-0923FAB77F0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fba5ec985bd82b3cac465db9033c3fdf19c29322
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824851"
---
# <a name="binding-minidrivers-to-the-hid-class"></a>将微型驱动程序绑定到 HID 类


本部分介绍系统提供的 HID 类驱动程序和 HID 微型驱动程序的操作，该操作支持 HIDClass[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)中的设备。

HID 类驱动程序提供了一个接口，上层驱动程序和用户模式应用程序使用该接口来访问输入设备支持的 HID 集合。 HID 类驱动程序使用 HID 微型驱动程序来访问输入设备的硬件。 HID 微型驱动程序抽象了输入设备连接到的总线端口的操作。 HID 类驱动程序是链接到 HID 微型驱动程序的导出驱动程序。 HID 微型驱动程序通过调用[**HidRegisterMinidriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hidport/nf-hidport-hidregisterminidriver)将其操作绑定到 hid 类驱动程序，将其操作绑定到 hid 类驱动程序。

HID 类驱动程序和 HID 微型驱动程序的组合操作充当输入设备的 WDM 函数驱动程序和输入设备支持的子设备（HID 集合）的总线驱动程序。 这种设计使 HID 类驱动程序可以操作连接到端口或总线（而不是 USB 总线）的 USB HID 设备和非 USB 输入设备。 基础父设备的操作细节对于上层驱动程序或用户模式应用程序而言是透明的。

 

 




