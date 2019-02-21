---
Description: Enumeration of USB Composite Devices
title: 枚举的复合的 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b38f5fbe18724afd558c7af665eac0c8aee3af5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534829"
---
# <a name="enumeration-of-usb-composite-devices"></a>枚举的复合的 USB 设备


当新的 USB 设备连接到主机计算机时，USB 总线驱动程序创建设备的物理设备对象 (PDO)，并生成报告新 PDO 的即插即用事件。 操作系统然后，查询的硬件 Id 与 PDO 相关联的总线驱动程序。

对于所有 USB 设备、 USB 总线驱动程序报告*设备 ID*具有以下格式：

`USB\VID_xxxx&PID_yyyy`

**请注意**  *xxxx*和*yyyy*直接取自**idVendor**并**idProduct**设备描述符字段分别。

 

总线驱动程序还会报告为兼容的标识符 (ID) 的`USB\COMPOSITE`，并且设备满足以下要求：

-   设备描述符的设备类字段 (**bDeviceClass**) 必须包含值为零或类 (**bDeviceClass**)，子类 (**bDeviceSubClass**)，并协议 (**bDeviceProtocol**) 的设备描述符字段必须具有值 0xEF、 0x02 和 0x01 中所述分别[USB 接口关联描述符](usb-interface-association-descriptor.md)。

-   设备必须具有多个接口。

-   设备必须具有单个配置。

总线驱动程序还会检查设备类 (**bDeviceClass**)，子类 (**bDeviceSubClass**)，和协议 (**bDeviceProtocol**) 的设备描述符字段。 如果这些字段均为零，则该设备是复合设备，总线驱动程序报告的 USB 额外兼容标识符 (ID)\\用于 PDO 复合。

在检索之后的硬件和兼容 Id 对新 PDO，操作系统搜索 INF 文件。 如果一个 INF 文件包含设备 ID 的匹配项，Windows 将加载该 INF 文件指示驱动程序和泛型父驱动程序不起作用。 如果没有 INF 文件包含设备 ID 和 PDO 具有兼容 ID，Windows 搜索兼容的 id。 这会生成 Usb.inf 中的匹配项，将导致操作系统加载[USB 通用父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)。

如果您希望泛型父驱动程序来管理你的设备，但你的设备不具有要确保系统将生成兼容的 USB ID 所需的特征\\组合键，您将需要提供加载泛型的 INF 文件父驱动程序。 INF 文件应包含需求/包括引用 Usb.inf 的部分。

如果复合设备具有多个配置，必须指定哪种配置提供的 INF 文件名泛型父应使用在注册表中。 必要的注册表项中所述[配置 Usbccgp.sys 选择非默认 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)。

## <a name="related-topics"></a>相关主题
[USB 泛型父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



