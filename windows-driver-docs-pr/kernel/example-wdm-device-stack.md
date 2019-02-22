---
title: 示例 WDM 设备堆栈
description: 示例 WDM 设备堆栈
ms.assetid: 1128e098-9ef4-4bc3-aa09-74df3142fb11
keywords:
- 设备堆栈 WDK 内核示例
- 游戏杆 WDK 设备堆栈
- 功能的设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 筛选器 DOs WDK 内核
- USB 集线器设备堆栈 WDK 内核
- USB 主机控制器设备堆栈 WDK 内核
- PCI 总线设备堆栈 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1d435c36f56ef93ccb9bbb09b705d26c601e314
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546951"
---
# <a name="example-wdm-device-stack"></a>示例 WDM 设备堆栈





本部分介绍用于说明 WDM 设备对象和分层方式的 USB 硬件的驱动程序的可能集合创建的设备对象。

下图显示了由中所述的示例驱动程序创建的设备对象[WDM 驱动程序层：示例](wdm-driver-layers---an-example.md)。

![说明示例 wdm 设备 usb 游戏杆对象层关系图](images/joydobj.png)

在此图中的底部，从开始，包括示例设备堆栈中的设备对象：

1.  PDO 和 PCI 总线 FDO。

    根总线驱动程序枚举的内部系统总线 （根总线），并创建为它找到的每个设备 PDO。 这些 PDOs 之一是为 PCI 总线。 （PDO 和根总线 FDO 不显示在图中。）

    PnP 管理器标识 PCI 驱动程序，如 PCI 总线功能驱动程序加载驱动程序 （如果尚未加载），并将 PDO 传递给 PCI 驱动程序。 在其[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程，PCI 驱动程序创建 PCI 总线 FDO ([**IoCreateDevice**](https://msdn.microsoft.com/library/windows/hardware/ff548397))，并将 FDO 附加到设备堆栈 ([**IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300)) 为 PCI 总线。 PCI 驱动程序创建，并将此 FDO 作为其职责的一部分作为 PCI 总线函数驱动程序。

    没有针对 PCI 总线在此示例中的筛选器驱动程序。

2.  PDO 和 USB 主控制器 FDO。

    即插即用经理指示要启动其设备的 PCI 驱动程序 ([**IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749))，然后为子查询 PCI 驱动程序 ([ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)关系类型为**BusRelations**)。 在响应中，PCI 驱动程序枚举其总线上的设备。 在此示例中，PCI 驱动程序查找 USB 主控制器，并创建该设备 PDO。 在图中的宽箭头表示 USB 主控制器 PCI 总线的"子级"。 PCI 驱动程序创建其子 PDOs 其职责的作为总线驱动程序的一部分为 PCI 总线的设备。

    PnP 管理器将 USB 主机控制器 miniclass/类驱动程序对标识为 USB 主控制器的功能驱动程序，并加载驱动程序对。 PnP 管理器在适当的时间来创建和附加 USB 主控制器 FDO 调用驱动程序对。

    没有针对 USB 主控制器在此示例中的筛选器驱动程序。

3.  PDO 和 USB 集线器 FDO。

    USB 主控制器枚举其总线、 定位 USB 集线器中的唯一端口，并创建一个为中心的 PDO。 USB 集线器驱动程序创建并附加 FDO 为中心。

    没有针对 USB 集线器，在此示例中的筛选器驱动程序。

4.  PDO、 FDO 和两个筛选器游戏杆设备的 DOs。

    USB 集线器驱动程序枚举其总线、 查找 HID 设备 （游戏杆），然后创建游戏杆 PDO。

    在此示例中，较低级别筛选器驱动程序具有已设置为游戏杆设备注册表中以便 PnP 管理器则加载筛选器驱动程序。 筛选器驱动程序确定它与设备相关和创建，并将执行操作的筛选器附加到设备堆栈。

    PnP 管理器确定游戏杆设备功能驱动程序是 HID 类/miniclass 驱动程序对加载这些驱动程序。 驱动程序对包含 miniclass 驱动程序链接到类驱动程序 DLL;结合在一起，它们将充当设备的一个功能驱动程序。 类/miniclass 驱动程序对创建一个设备对象，FDO，并将其附加到设备堆栈。

    较高级别筛选器驱动程序创建，并将执行操作的筛选器附加到设备堆栈，以类似于较低级别筛选器的方式。

请注意，创建父总线驱动程序的 PDO 始终在特定设备的设备堆栈的底部。 当处理即插即用驱动程序或 power Irp，它们必须一直向设备堆栈下的每个 IRP 传递给 PDO 和其关联的总线驱动程序。

下图显示了上图中，作为同一设备堆栈，但强调的设备对象是由创建和管理哪些驱动程序。

![说明示例设备对象从驱动程序的角度来看的层关系图](images/joydobj2.png)

总线驱动程序跨多个设备堆栈。 总线驱动程序创建其总线适配器/控制器 FDO 和一个 PDO 其子级的每个设备。

 

 




