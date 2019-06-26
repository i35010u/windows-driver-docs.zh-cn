---
title: 安装 HID 客户端
description: 本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。
ms.assetid: 080992B1-AB36-4BA1-BF44-7CF0C9F4EEE3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 391539f4f21323fc27ee4977766954347adbb029
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375912"
---
# <a name="installing-hid-clients"></a>安装 HID 客户端


本部分介绍在 Microsoft Windows 中安装 HIDClass 设备的以下要求。

-   必须使用供应商[*硬件 Id* ](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)的顶级集合的指定为*供应商的硬件 ID 格式*中[HIDClass 的硬件 Id顶级集合](hidclass-hardware-ids-for-top-level-collections.md)。

-   父 （下方 HIDClass 设备的驱动程序堆栈中的 HID 类驱动程序安装） 的输入设备的供应商提供驱动程序必须提供的 HID 类驱动程序使用生成的顶级集合的硬件 Id 的硬件信息。 （请注意，HIDClass 设备的系统提供的驱动程序自动执行此操作。）

-   在 Windows Vista 和更高版本的 Windows 中，供应商可以启用 USB HID 设备的选择性挂起功能。 此功能定义的修订版本 2.0 中*通用串行总线规范。* 详细了解 Windows 如何支持 USB 选择性挂起功能，请参阅[USB 选择性挂起](../usbcon/usb-selective-suspend.md)。

没有安装 HIDClass 设备的其他特定于 HIDClass 的要求。 有关如何安装设备的详细信息，请参阅[设备安装概述](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-and-driver-installation)。

 

 




