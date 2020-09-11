---
description: USB 复合设备上的描述符
title: USB 复合设备上的描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41c71bca6c444b311a7d359d0dc7da37b02869be
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009801"
---
# <a name="descriptors-on-usb-composite-devices"></a>USB 复合设备上的描述符


如 USB 规范所述，每个 USB 设备都提供一组定义其功能的分层描述符。 在顶级，每个设备都有一个或多个 USB 配置描述符，其中每个都有一个或多个接口描述符。 有关 USB 配置描述符的详细信息，请参阅 [Usb 配置描述符](usb-configuration-descriptors.md)。 配置是互相排斥的，因此，一次只能选择一个配置来操作。

在 Windows Vista 之前，Microsoft 提供的驱动程序只选择 "配置 1"。 在 Windows Vista 和更高版本的 Windows 中，你可以设置注册表值以指定 [USB 通用父驱动程序 ( # A0) ](usb-common-class-generic-parent-driver.md) 将使用哪种配置。 有关在复合设备上选择设备配置的详细信息，请参阅 [如何为 USB 设备选择配置](how-to-select-a-configuration-for-a-usb-device.md)。

在配置中，接口和接口集合是独立管理的。 每个接口都按其[**USB \_ 接口 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)结构的**bInterfaceNumber**成员中的唯一值在描述符级别表示。

接口的功能由相同结构的 **bInterfaceClass**、 **bInterfaceSubClass**和 **bInterfaceProtocol** 成员以及可能跟随它的类特定说明符指示。

有关描述符的详细信息，请参阅 [USB 描述符](usb-descriptors.md)。

## <a name="related-topics"></a>相关主题
[USB 常规父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)