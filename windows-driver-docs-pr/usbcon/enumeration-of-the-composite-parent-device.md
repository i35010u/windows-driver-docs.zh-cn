---
description: 枚举 USB 复合设备
title: 枚举 USB 复合设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f897303030f813ce046f28668d041ee374a70887
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968558"
---
# <a name="enumeration-of-usb-composite-devices"></a>枚举 USB 复合设备


当新的 USB 设备连接到主机时，USB 总线驱动程序会为设备创建 (PDO) 的物理设备对象，并生成 PnP 事件来报告新的 PDO。 然后，操作系统会在总线驱动程序中查询与 PDO 关联的硬件 Id。

对于所有 USB 设备，USB 总线驱动程序使用以下格式报告 *设备 ID* ：

`USB\VID_xxxx&PID_yyyy`

**请**分别从 " **idVendor** " 和 " **idProduct** " 字段中提取  *xxxx*和*yyyy* 。

 

`USB\COMPOSITE`如果设备满足以下要求，则总线驱动程序还会报告兼容的标识符 (ID) ：

-   设备描述符 (**bDeviceClass**) 的 "设备类" 字段必须包含零值，或 "类 (**bDeviceClass**) "、"子类 (**bDeviceSubClass**) " 和 "协议 (**bDeviceProtocol** "。设备描述符的 ") " 字段的值必须分别为0XEF、0X02 和0x01，如 [USB 接口关联描述符](usb-interface-association-descriptor.md)中所述。

-   设备必须有多个接口。

-   设备必须具有一个配置。

总线驱动程序还会检查设备类 (**bDeviceClass**) 、子类 (**bDeviceSubClass**) 和协议 (**bDeviceProtocol**) 的设备描述符字段。 如果这些字段为零，则该设备为复合设备，并且总线驱动程序会报告 PDO (ID) 的其他兼容标识符 \\ 。

检索新 PDO 的硬件和兼容 Id 后，操作系统会搜索 INF 文件。 如果其中一个 INF 文件包含设备 ID 的匹配项，则 Windows 将加载该 INF 文件所指示的驱动程序，并且不会播放一般父驱动程序。 如果没有 INF 文件包含设备 ID，并且 PDO 具有兼容的 ID，则 Windows 将搜索兼容 ID。 这会在 Usb 中生成匹配项，并导致操作系统加载 [ ( # A0) 的 Usb 通用父驱动程序 ](usb-common-class-generic-parent-driver.md)。

如果你希望通用父驱动程序管理你的设备，但你的设备不具有确保系统将生成兼容 USB 复合 ID 的必要特征 \\ ，则必须提供加载通用父驱动程序的 INF 文件。 INF 文件应包含引用 Usb .inf 的 "需要/包括" 部分。

如果复合设备有多个配置，则提供的 INF 文件必须指定一般父项应在注册表中使用的配置。 将 [Usbccgp.sys 配置为选择非默认的 USB 配置](selecting-the-configuration-for-a-multiple-interface--composite--usb-d.md)中介绍了必需的注册表项。

## <a name="related-topics"></a>相关主题
[USB 常规父驱动程序 (Usbccgp.sys)](usb-common-class-generic-parent-driver.md)  
[Microsoft 提供的 USB 驱动程序](system-supplied-usb-drivers.md)  



