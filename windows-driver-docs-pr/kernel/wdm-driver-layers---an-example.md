---
title: WDM 驱动程序层示例
description: WDM 驱动程序层示例
keywords:
- WDM 驱动程序 WDK 内核，分层驱动程序
- 分层驱动程序 WDK 内核
- 驱动程序层 WDK WDM
- 游戏杆 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: de6e55aea53eacfe059ed095716a8a4b449fd7dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792694"
---
# <a name="wdm-driver-layers-an-example"></a>WDM 驱动程序层：一个示例





本部分介绍了一组可能的适用于 USB 硬件的 WDM 驱动程序，以说明 WDM 驱动程序层。

下图显示了一个 USB 游戏杆的 PnP 硬件配置示例。

![阐释 usb 游戏杆的即插即用硬件示例的示意图](images/usbjoyhw.png)

在此图中，USB 操纵杆插入 USB 集线器上的端口。 此示例中的 USB 集线器位于 USB 主机控制器板上，并插入到 USB 主机控制器板上的单个端口。 USB 主机控制器插入 PCI 总线。 从 PnP 的角度来看，USB 集线器、USB 主机控制器和 PCI 总线都是总线设备，因为每个设备都提供端口。 操纵杆不是总线设备。

下图显示了一个示例驱动程序集，可能会为上图中的 USB 游戏杆硬件加载这些驱动程序集。

![阐释 usb 游戏杆的即插即用驱动程序层的示意图](images/usbjoydr.png)

从上图的底部开始，示例堆栈中的驱动程序包括：

-   驱动 PCI 总线的 PCI 驱动程序。 这是一个 PnP 总线驱动程序。 PCI 总线驱动程序随 Microsoft 提供系统。

-   USB 主机控制器的总线驱动程序作为类/miniclass 驱动程序对实现。 Microsoft 提供了 USB 主机控制器类和 miniclass 驱动程序。

-   驱动 USB 集线器的 USB 集线器总线驱动程序。 USB 集线器驱动程序随 Microsoft 提供。

-   游戏杆设备的三个驱动程序;其中一个是类/miniclass 对。

    功能驱动程序（操纵杆设备的主驱动程序）是 HID 类驱动程序/HID USB miniclass 驱动程序对。  (HID 表示 "人体学接口设备"。 ) HID USB miniclass 驱动程序支持 HID 设备的特定于 USB 的语义，并依赖于 HID 类驱动程序 DLL 以获取一般 HID 支持。

    函数驱动程序可以特定于特定设备，也可以是在使用 HID 时，函数驱动程序可以为一组设备服务。 在此示例中，HID 类驱动程序/HID USB miniclass 驱动程序对将 USB 总线上系统中的所有符合 HID 标准的设备服务。 HID 类驱动程序/HID 1394 miniclass 驱动程序对将在1394总线上为任何符合 HID 标准的设备服务。

    函数驱动程序可以由设备供应商或 Microsoft 编写。 在此示例中， (写入 HID 类/HID USB miniclass 驱动程序对的函数驱动程序) 。

    在此示例中有两个用于操纵杆设备的筛选器驱动程序：添加宏按钮功能的顶级类筛选器，以及使操纵杆能够模拟鼠标设备的较低级别的设备筛选器。

    顶级筛选器由需要筛选操纵杆 i/o 的人员编写，较低级别的筛选器驱动程序由操纵杆供应商编写。

-   内核模式和用户模式 HID 客户端和应用程序不是驱动程序，而是为了完整性而显示。

 

 




