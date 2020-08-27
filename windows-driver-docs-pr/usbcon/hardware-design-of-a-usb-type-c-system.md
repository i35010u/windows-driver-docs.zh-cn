---
description: 下面是 USB 类型 C 系统的一些示例设计。
title: USB 类型 C 系统的硬件设计
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36f68a1ddd61869724811049f62d453ad3f67122
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969488"
---
# <a name="hardware-design-usb-type-c-systems"></a>硬件设计：USB 类型 C 系统


**上次更新时间**

-   2016 年 12 月

\[某些信息与预发布的产品相关，这些信息可能会在正式发布之前进行重大修改。 对于此处提供的信息，Microsoft 不作任何明示或暗示的担保。\]

下面是 USB 类型 C 系统的一些示例设计。

典型的 USB 类型 C 系统包含以下组件：

-   **USB 双重角色控制器** 可以在主机角色或功能/设备/外设角色中操作。 此组件集成到 SoC。
-   在某些 Soc 中，可能会集成**电池充电1.2 检测**。 某些 SoC 供应商提供了一个 PMIC 模块，该模块实现了检测逻辑，其他人在软件中实现。 Windows 10 移动版支持所有这些选项。 请与 SoC 供应商联系以获取有关此组件的详细信息。
-   **类型-c-PD 端口控制器** 管理 USB 类型 c 连接器上的 CC pin。 支持对电源传送消息进行 BMC 编码/解码。 在大多数 Soc 中，此组件通常不集成。
-   **Mux** 根据类型 C 端口控制器检测到的方向，将 USB 对 SuperSpeed 到控制器上的端口。 Mux SuperSpeed 对和可能在其他地方使用的 SBU 行 (通常是在进入备用模式时) 显示模块。
-   **VBus/VConn** 源是必需的。 大多数 PMICs 实现 VBus/VConn 控件。 有关详细信息，请联系 SoC/PMIC 供应商。

## <a name="usb-type-c-system-design-with-an-embedded-controller"></a><a href="" id="emb"></a>使用嵌入式控制器的 USB 类型 C 系统设计


除了上述列表中的组件，USB 类型 C 系统还可以有嵌入的控制器。 此智能微控制器作为系统的类型 C 和电源交付策略管理器。

下面是带有嵌入式控制器的 USB 类型 C 系统的示例：

![usb 类型 c 硬件设计示例嵌入式控制器设备](images/type-c-hw1.png)

下面是另一个视图：

![usb 类型 c 硬件设计示例嵌入式控制器设备](images/type-c-hw1-1.png)

对于具有嵌入控制器的系统，请加载 Microsoft 提供的内置驱动程序 UcmUcsi.sys，该驱动程序实现 USB 类型 C 连接器系统软件接口 (UCSI) 规范。

[UCSI 驱动程序](ucsi.md)。 有关为驱动程序加载的设备堆栈的信息，请参阅 [支持 USB Type-C 组件的驱动程序（适用于具有嵌入式控制器的系统](architecture--usb-type-c-in-a-windows-system.md#drivers)）。


适用于具有使用非 ACPI 传输的嵌入式控制器的系统。 

[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)

[USB 类型 C 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

## <a name="usb-type-c-system-design"></a><a href="" id="hardware"></a>USB 类型 C 系统设计


下面是没有嵌入控制器的移动设备的 USB 类型 C 系统示例：

![用于移动设备的 usb 类型 c 硬件设计示例](images/type-c-hw2.png)

下面是另一个视图：

![usb 类型-c 硬件设计示例设备没有嵌入控制器](images/type-c-hw2-1.png)

对于前面的设计，实现了与连接器通信的驱动程序，并使操作系统知道连接器上的 USB 类型 C 事件。

[编写 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)

[USB 类型 C 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

## <a name="related-topics"></a>相关主题
[Windows 对 USB 类型 C 连接器的支持](oem-tasks-for-bringing-up-a-usb-typec.md)  



