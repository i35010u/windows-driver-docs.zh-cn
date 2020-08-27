---
description: 本部分介绍 Microsoft 为复合设备提供的 Usbccgp.sys 驱动程序。
title: USB 常规父驱动程序 (Usbccgp.sys)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eec142f567fe1afcaab1ca740d70cf6e6e477a2
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969596"
---
# <a name="usb-generic-parent-driver-usbccgpsys"></a>USB 常规父驱动程序 (Usbccgp.sys)


本部分介绍 Microsoft 为复合设备提供的 Usbccgp.sys 驱动程序。

许多 USB 设备公开多个 *usb 接口*。 在 USB 术语中，这些设备称为 *复合设备*。 Microsoft Windows 2000 和 Windows 98 操作系统包含 USB 总线驱动程序中的通用父设施 ( # A0) 将复合设备的每个接口公开为单独的设备。 在 Microsoft Windows XP 和 Windows Me 中，此功能通过将其传输到称为 *USB 通用父驱动程序* 的独立驱动程序 ( # A0) 来简化和改进。 使用通用父驱动程序的功能，设备供应商可以对某些接口选择性地使用 Microsoft 提供的驱动程序支持。

某些复合设备的接口独立运行。 例如，带有电源按钮的复合 USB 键盘可能有一个键盘接口，还有一个用于电源按钮的接口。 USB 通用父驱动程序将每个接口枚举为单独的设备。 操作系统加载 Microsoft 提供的键盘驱动程序来管理键盘接口，并加载 Microsoft 提供的电源密钥驱动程序以管理电源密钥接口。

如果复合设备具有本机 Windows 驱动程序不支持的接口，则该设备的供应商应为接口和 INF 文件提供驱动程序。 INF 文件应具有与接口的设备 ID 匹配的 INF *DDInstall* 部分。 INF 文件不能与复合设备本身的设备 ID 匹配，因为这会阻止通用父驱动程序加载。 有关操作系统如何加载 USB 通用父驱动程序的说明，请参阅 [Usb 复合设备的枚举](enumeration-of-the-composite-parent-device.md)。

某些设备将接口组合到一起工作以执行特定*功能*的*接口集合*。 当接口在接口集合中分组时，一般父驱动程序将每个集合（而不是每个单独的接口）视为一个设备。 有关泛型父驱动程序如何管理接口集合的详细信息，请参阅 [USB 复合设备上的接口集合枚举](support-for-interface-collections.md)。

操作系统加载复合设备接口的客户端驱动程序之后，一般父驱动程序将从客户端驱动程序多路复用数据流，并将这些单独的交互合并为复合设备的单个数据流。 一般父代为整个复合设备及其所有接口的电源策略所有者。 它还管理同步和 PnP 请求。

如果 Microsoft 提供的驱动程序支持某些接口，而通用父驱动程序可以简化复合硬件供应商的任务。 此类设备的供应商只需为不受支持的接口提供驱动程序，因为通用父驱动程序有助于为支持的接口使用 Microsoft 提供的驱动程序。

以下各节介绍通用父驱动程序的特性和功能：

[枚举 USB 复合设备](enumeration-of-the-composite-parent-device.md)

[USB 复合设备上的描述符](descriptors-on-composite-usb-devices.md)

[枚举 USB 复合设备上的接口](enumeration-of-interfaces-not-grouped-in-collections.md)

[枚举 USB 复合设备上的接口集合](support-for-interface-collections.md)

[Usbccgp.sys 中的内容安全功能](content-security-features-in-the-composite-client-generic-parent-drive.md)

## <a name="related-topics"></a>相关主题
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



