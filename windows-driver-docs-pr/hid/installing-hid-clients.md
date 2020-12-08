---
title: 安装 HID 客户端
description: 本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c225973e108c6ea5f4111f1a71ca314cf119c55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796213"
---
# <a name="installing-hid-clients"></a>安装 HID 客户端


本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。

-   供应商必须使用在 HIDClass 硬件 Id 中指定为 *供应商硬件 id 格式* 的顶级集合的 [*硬件 Id*](../install/hardware-ids.md) [才能 Top-Level 集合](hidclass-hardware-ids-for-top-level-collections.md)。

-   供应商为父输入设备提供的驱动程序 (安装在 HIDClass 设备的驱动程序堆栈中的 HID 类驱动程序下) 必须提供 HID 类驱动程序为顶级集合生成硬件 Id 时所用的硬件信息。  (请注意，系统提供的 HIDClass 设备驱动程序会自动执行此操作。 ) 

-   在 Windows Vista 和更高版本的 Windows 中，供应商可以为 USB HID 设备启用选择性挂起功能。 此功能在 *通用串行总线规范* 的修订版2.0 中定义。 有关 Windows 如何支持 USB 选择性挂起功能的详细信息，请参阅 [usb 选择性挂起](../usbcon/usb-selective-suspend.md)。

对于安装 HIDClass 设备，没有其他特定于 HIDClass 的要求。 有关如何安装设备的详细信息，请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md)。

 

