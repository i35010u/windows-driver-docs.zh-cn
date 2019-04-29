---
Description: 以下是一些示例设计为 USB C 类型系统。
title: USB C 类型系统的硬件设计
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44a2677550b5c56a958b77a9af31ec3844a8263d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371844"
---
# <a name="hardware-design-usb-type-c-systems"></a>硬件设计：USB 类型 C 系统


**上次更新时间**

-   2016 年 12 月

\[有些信息与预发布产品的商业发布之前可能有大幅度修改。 Microsoft 不做任何明示或暗示的担保，此处提供的信息。\]

以下是一些示例设计为 USB C 类型系统。

典型的 USB C 类型系统中有这些组件：

-   **USB 双角色控制器**能够操作主机角色中或外围设备设备/函数/角色中。 此组件集成到 SoC.
-   **电池充电 1.2 检测**可能集成到某些 Soc 中。 某些 SoC 供应商提供了实现检测逻辑的 PMIC 模块、 其他人在软件中实现。 Windows 10 移动版支持所有这些选项。 请联系 SoC 供应商联系以获取有关此组件的详细信息。
-   **类型 C PD 端口控制器**管理 USB 类型 C 连接器上的抄送插针。 支持 BMC 编码/解码的 power 传递消息。 在大多数 Soc 中通常不集成此组件。
-   **Mux** SuperSpeed USB 对根据方向由类型 C 端口控制器检测到的控制器上的端口。 Mux SuperSpeed 对，并且可能是 SBU 行其他位置 （通常显示模块） 时进入备用模式。
-   **VBus/VConn**源是必需的。 大多数 PMICs 实现 VBus/VConn 控件。 有关详细信息，请与你 SoC/PMIC 的供应商联系。

## <a href="" id="emb"></a>使用嵌入式控制器进行 USB 类型 C 系统设计


除了上述列表中的组件，USB 类型 C 系统都可能具有嵌入式的控制器。 此智能微控制器作为系统的类型 C 和 Power 传递策略管理器。

下面是具有嵌入式控制器的 USB C 类型系统的示例：

![适用于嵌入式的控制器设备的 usb 类型 c 硬件设计示例](images/type-c-hw1.png)

下面是另一个视图：

![适用于嵌入式的控制器设备的 usb 类型 c 硬件设计示例](images/type-c-hw1-1.png)

对于具有嵌入式的控制器的系统，加载 Microsoft 提供的现成驱动程序 UcmUcsi.sys，实现 USB 类型 C 连接器系统软件接口 (UCSI) 规范。

[UCSI 驱动程序](ucsi.md)。 有关加载的驱动程序的设备堆栈的信息，请参阅[驱动程序支持 USB 类型 C 组件为系统使用嵌入控制器](architecture--usb-type-c-in-a-windows-system.md#drivers)。


有关使用非 ACPI 传输的嵌入式的控制器的系统。 

[编写 UCSI 客户端驱动程序](write-a-ucsi-driver.md)

[USB 类型 C 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

## <a href="" id="hardware"></a>USB 类型 C 系统设计


下面是不具有嵌入式的控制器的移动设备的 USB C 类型系统的示例：

![移动设备的的 usb 类型 c 硬件设计示例](images/type-c-hw2.png)

下面是另一个视图：

![如果没有嵌入控制器 usb 类型 c 硬件设计示例设备](images/type-c-hw2-1.png)

对于前面的设计，实现与连接器通信，并保留有关 USB 类型 C 事件通知在连接器上的操作系统的驱动程序。

[编写 USB 类型 C 连接器驱动程序](bring-up-a-usb-type-c-connector-on-a-windows-system.md)

[USB 类型 C 驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

## <a name="related-topics"></a>相关主题
[Windows 支持 USB 类型 C 连接器](oem-tasks-for-bringing-up-a-usb-typec.md)  



