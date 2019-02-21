---
Description: This section describes the Usbccgp.sys driver provided by Microsoft for composite devices.
title: USB 泛型父驱动程序 (Usbccgp.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0ecd4e815027c763921b339e3c0fb20b4f41867
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526728"
---
# <a name="usb-generic-parent-driver-usbccgpsys"></a>USB 泛型父驱动程序 (Usbccgp.sys)


本部分介绍由 Microsoft 提供的复合设备 Usbccgp.sys 驱动程序。

很多 USB 设备公开多个*USB 接口*。 这些设备在 USB 术语中称为*复合设备*。 Microsoft Windows 2000 和 Windows 98 的操作系统包括 USB 总线驱动程序中 (Usbhub.sys) 公开该复合设备是一个单独的设备的每个接口的泛型父设施。 在 Microsoft Windows XP 和 Windows Me 中，简化并改进了通过将它传输到独立的驱动程序调用此工具*USB 泛型父驱动程序*(Usbccgp.sys)。 使用泛型父驱动程序的功能，设备供应商可以进行一些接口的选择性使用 Microsoft 提供的驱动程序支持。

独立运行的一些复合设备接口。 例如，带电源按钮的复合 USB 键盘可能有一个接口适用于键盘和的电源按钮的另一个接口。 USB 泛型父驱动程序会枚举这些接口的每个作为一个单独的设备。 Microsoft 提供键盘驱动程序管理键盘界面和 Microsoft 提供 power 密钥驱动程序来管理电源密钥接口加载操作系统。

如果复合设备具有本机 Windows 驱动程序不支持的接口，设备的供应商应提供一个驱动程序接口和一个 INF 文件。 INF 文件应具有 INF *DDInstall*接口设备 ID 相匹配的部分。 INF 文件不得匹配复合设备本身，设备 ID，因为这会阻止加载泛型父驱动程序。 操作系统加载 USB 泛型父驱动程序的方式的说明，请参阅[枚举的 USB 复合设备](enumeration-of-the-composite-parent-device.md)。

到某些设备组接口*接口集合*协同工作以执行特定*函数*。 当接口分为不同的接口集合时，泛型父驱动程序将每个集合，而不是每个单独的接口，处理为设备。 有关泛型父驱动程序管理接口集合的方式的详细信息，请参阅[枚举的接口集合 USB 复合设备上](support-for-interface-collections.md)。

操作系统加载的复合设备接口的客户端驱动程序后，泛型父驱动程序多路复用客户端驱动程序，合并到单个数据流复合设备的这些单独交互的数据流。 泛型的父级是整个复合设备和其所有接口的电源策略所有者。 它还管理同步和即插即用的请求。

如果 Microsoft 提供的驱动程序支持某些接口而不是其他泛型父驱动程序可以简化的复合硬件供应商的任务工作。 此类设备的供应商只需要提供驱动程序不受支持的接口，因为泛型父驱动程序便于使用 Microsoft 提供的驱动程序的受支持的接口。

以下部分介绍的特性和功能的泛型父驱动程序：

[枚举的复合的 USB 设备](enumeration-of-the-composite-parent-device.md)

[在 USB 复合设备上的描述符](descriptors-on-composite-usb-devices.md)

[复合的 USB 设备上的接口的枚举](enumeration-of-interfaces-not-grouped-in-collections.md)

[复合的 USB 设备上的接口集合的枚举](support-for-interface-collections.md)

[Usbccgp.sys 中的内容的安全功能](content-security-features-in-the-composite-client-generic-parent-drive.md)

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



