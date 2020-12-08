---
title: 示例 WDM 设备堆栈
description: 示例 WDM 设备堆栈
keywords:
- 设备堆栈 WDK 内核，示例
- 游戏杆 WDK 设备堆栈
- 功能设备对象 WDK 内核
- FDO WDK 内核
- 物理设备对象 WDK 内核
- PDOs WDK 内核
- 筛选 DOs WDK 内核
- USB 集线器设备堆栈 WDK 内核
- USB 主机控制器设备堆栈 WDK 内核
- PCI 总线设备堆栈 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b61745bc5179b81a4decbb735ddefb5fa8d6d5af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793575"
---
# <a name="example-wdm-device-stack"></a>示例 WDM 设备堆栈





本部分介绍了一组可能的 USB 硬件驱动程序所创建的设备对象，以说明 WDM 设备对象以及这些对象如何分层。

下图显示了 [WDM 驱动程序层](wdm-driver-layers---an-example.md)中所述的示例驱动程序所创建的设备对象：示例。

![阐释 usb 游戏杆的示例 wdm 设备对象层的示意图](images/joydobj.png)

从此图的底部开始，示例设备堆栈中的设备对象包括：

1.  适用于 PCI 总线的 PDO 和 FDO。

    根总线驱动程序枚举 (根总线) 的内部系统总线，并为它找到的每个设备创建一个 PDO。 其中一种 PDOs 适用于 PCI 总线。  (根总线的 PDO 和 FDO 不显示在图中。 ) 

    PnP 管理器将 PCI 驱动程序标识为 PCI 总线的函数驱动程序，将驱动程序加载到 (（如果尚未加载）) ，并将 PDO 传递到 PCI 驱动程序。 在其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程中，pci 驱动程序为 pci bus () [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice) 创建 FDO，并将 FDO 附加到 pci 总线 ([**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)) 的设备堆栈。 PCI 驱动程序会创建此 FDO 并将其作为其职责的一部分附加，作为 PCI 总线的函数驱动程序。

    在此示例中，PCI 总线没有筛选器驱动程序。

2.  USB 主机控制器的 PDO 和 FDO。

    PnP 管理器指示 PCI 驱动程序启动其设备 ([**IRP \_ MN \_ start \_ device**](./irp-mn-start-device.md)) ，然后 ([**irp \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md) （与 **BusRelations**) 关系类型）查询 pci 驱动程序的子驱动程序。 作为响应，PCI 驱动程序会枚举其总线上的设备。 在此示例中，PCI 驱动程序找到 USB 主机控制器并为该设备创建 PDO。 图中的宽箭头表示 USB 主机控制器是 PCI 总线的 "子级"。 PCI 驱动程序会创建其子设备的 PDOs 作为其责任的一部分作为 PCI 总线的总线驱动程序。

    PnP 管理器将 USB 主机控制器 miniclass/类驱动程序对标识为 USB 主机控制器的函数驱动程序并加载驱动程序对。 PnP 管理器会在适当的时间调用驱动程序对，以创建并附加 USB 主机控制器的 FDO。

    在此示例中，USB 主机控制器没有筛选器驱动程序。

3.  USB 集线器的 PDO 和 FDO。

    USB 主机控制器枚举其总线，在唯一端口中查找 USB 集线器，并为集线器创建 PDO。 USB 集线器驱动程序为集线器创建并附加 FDO。

    在此示例中，USB 集线器没有筛选器驱动程序。

4.  操纵杆设备的 PDO、FDO 和两个筛选器 DOs。

    USB 集线器驱动程序会枚举其总线， (操纵杆) 找到 HID 设备，并为操纵杆创建一个 PDO。

    在此示例中，为操纵杆设备在注册表中设置了一个较低级别的筛选器驱动程序，因此 PnP 管理器会加载筛选器驱动程序。 筛选器驱动程序确定它与设备相关，并创建筛选器并将其附加到设备堆栈。

    PnP 管理器会确定操纵杆设备的函数驱动程序为 HID 类/miniclass 驱动程序对，并加载这些驱动程序。 驱动程序对包含链接到类驱动程序 DLL 的 miniclass 驱动程序;它们共同作用于设备的一个函数驱动程序。 类/miniclass 驱动程序对创建一个设备对象（FDO），并将其附加到设备堆栈。

    上层筛选器驱动程序创建筛选器并将其附加到设备堆栈，其方式类似于较低级别的筛选器。

请注意，父总线驱动程序创建的 PDO 始终位于特定设备的设备堆栈的底部。 当驱动程序处理 PnP 或 power Irp 时，它们必须将每个 IRP 向下传递到 PDO 及其关联的总线驱动程序。

下图显示了与上图相同的设备堆栈，但强调了哪些设备对象是由哪些驱动程序创建和管理的。

![从驱动程序的角度演示示例设备对象层的关系图](images/joydobj2.png)

总线驱动程序跨多个设备堆栈。 总线驱动程序为其总线适配器/控制器创建 FDO，并为其每个子设备创建一个 PDO。

 

