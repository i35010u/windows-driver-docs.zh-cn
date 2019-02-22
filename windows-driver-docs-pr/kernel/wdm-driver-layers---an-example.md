---
title: WDM 驱动程序层示例
description: WDM 驱动程序层示例
ms.assetid: 64eaa850-6394-4832-b11f-ce4db7f7c37d
keywords:
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 游戏杆 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b96e7151fda11e11b001f074eb3792b9b2f4639d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526892"
---
# <a name="wdm-driver-layers-an-example"></a>WDM 驱动程序层：示例





本部分介绍 USB 硬件来说明 WDM 驱动程序层的 WDM 驱动程序的可能集合。

下图显示了 USB 游戏杆的示例即插即用硬件配置。

![usb 游戏杆的演示示例插硬件的关系图](images/usbjoyhw.png)

在此图中，USB 游戏杆插入到 USB 集线器上的端口。 在此示例中的 USB 集线器位于 USB 主控制器板上，插入 USB 主机控制器板上的单一端口。 PCI 总线会插入 USB 主控制器。 从即插即用的角度来看、 USB 集线器、 USB 主控制器和 PCI 总线是总线的所有设备，因为它们分别提供端口。 游戏杆不是总线设备。

下图显示了示例集可能加载在上图中的 USB 游戏杆硬件的驱动程序。

![说明示例插 usb 游戏杆驱动程序层关系图](images/usbjoydr.png)

在上图中的底部，从开始，在该示例堆栈中的驱动程序包括：

-   驱动器 PCI 总线 PCI 驱动程序。 这是即插即用总线驱动程序。 PCI 总线驱动程序是由 Microsoft 提供与系统。

-   作为一类/miniclass 驱动程序对实现 USB 主控制器的总线驱动程序。 USB 主控制器类和 miniclass 驱动程序由 Microsoft 提供与系统中。

-   USB 集线器总线驱动程序驱动 USB 集线器。 USB 集线器驱动程序是由 Microsoft 提供与系统。

-   游戏杆设备; 的三个驱动程序其中一个是类/miniclass 对。

    功能驱动程序、 游戏杆设备的主要驱动程序是 HID 类驱动程序/HID USB miniclass 驱动程序对。 （HID 表示"人体学接口设备"。）HID USB miniclass 驱动程序支持依赖于常规的 HID 支持的 HID 类驱动程序 DLL 的 HID 设备的特定于 USB 的语义。

    功能驱动程序可以是特定于特定设备，或者，如下所示 hid 标准的情况下，功能驱动程序可以提供服务的一组设备。 在此示例中，HID 类驱动程序/HID USB miniclass 驱动程序对 USB 总线上的系统中的服务任何符合 hid 标准的设备。 HID 类驱动程序/HID 1394 miniclass 驱动程序对将服务的 1394年总线上任何符合 hid 标准的设备。

    由设备供应商或 microsoft 可以编写功能驱动程序。 在此示例中，功能驱动程序由 Microsoft 编写 （的 HID 类/HID USB miniclass 驱动程序对）。

    有两个筛选器在此示例中的游戏杆设备驱动程序： 添加宏按钮功能和较低级别设备筛选器的较高级别类筛选器使游戏杆来模拟鼠标设备。

    较高级别筛选器的人需要写入到筛选器的游戏杆 I/O 和较低级别筛选器驱动程序编写游戏杆供应商。

-   内核模式和用户模式下 HID 客户端和应用程序不是驱动程序，但出于完整性的考虑所示。

 

 




