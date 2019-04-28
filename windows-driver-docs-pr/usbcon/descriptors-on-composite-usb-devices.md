---
Description: 在 USB 复合设备上的描述符
title: 在 USB 复合设备上的描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3b5c38a1a35404fc3c9bb6612fa81d9f374f1e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352605"
---
# <a name="descriptors-on-usb-composite-devices"></a>在 USB 复合设备上的描述符


如 USB 规范中所述，每个 USB 设备提供了一系列定义其功能的分层描述符。 最高级别每个设备都有一个或多个 USB 配置描述符，每个都有一个或多个接口描述符。 有关 USB 配置描述符的进一步信息，请参阅[USB 配置描述符](usb-configuration-descriptors.md)。 配置是互斥的因此，只有一个配置，可以选择要一次操作。

Windows Vista 以前的 Microsoft 提供的驱动程序只能选择配置 1。 在 Windows Vista 和更高版本的 Windows 中，可以设置注册表值以指定的配置[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)将使用。 有关选择复合设备上的设备配置的详细信息，请参阅[如何为 USB 设备选择一个配置](how-to-select-a-configuration-for-a-usb-device.md)。

在配置中，接口和接口集合是单独管理。 每个接口表示，级别的描述符中的唯一值来**bInterfaceNumber**的成员及其[ **USB\_接口\_描述符**](https://msdn.microsoft.com/library/windows/hardware/ff540065)结构。

接口的函数将由**bInterfaceClass**， **bInterfaceSubClass**，并**bInterfaceProtocol**成员相同的结构，以及与可以按照它的特定于类的描述符。

描述符的详细信息，请参阅[USB 描述符](usb-descriptors.md)。

## <a name="related-topics"></a>相关主题
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



