---
title: USB 大容量存储设备的设备对象示例
description: USB 大容量存储设备的设备对象示例
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- USB 大容量存储设备示例 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27181738fb6275958cb60ee0b6e13c2291c735fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804697"
---
# <a name="device-object-example-for-a-usb-mass-storage-device"></a>USB 大容量存储设备的设备对象示例


## <span id="ddk_device_object_example_for_a_usb_mass_storage_device_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_USB_MASS_STORAGE_DEVICE_KG"></span>


下图显示了为组合 USB 大容量存储设备创建的、包含智能媒体槽和袖珍闪存槽的设备对象。

![为复合 USB 大容量存储设备创建的设备对象，其中包含智能媒体槽和袖珍闪存槽](images/usbstor.png)

复合 USB 大容量存储设备的设备对象树

从图的底部开始，下表描述了每个设备对象或设备对象堆栈及其关联的驱动程序：

1.  PCI 总线驱动程序枚举 USB 主机控制器。 系统会加载端口驱动程序、 *usbport.sys* 及其随附的微型端口 (，如图) 所示。 然后， *usbport.sys* 为主机控制器创建一个 FDO。

2.  端口驱动程序从根集线器开始枚举系统中的 USB 集线器。 *usbhub.sys* 驱动程序管理所有的 USB 集线器。 此图仅显示了一个级别的中心设备对象，但 USB 允许集线器设备的菊花链，因此树中可能会有更多的中心设备对象。 集线器驱动程序检测并枚举 USB 大容量存储设备，并为其创建 PDO。

3.  Windows 提供了一个 USB 存储端口驱动程序， *usbstor.sys*，它充当 usb stack 和本机 Windows 存储类驱动程序之间的接口。 USB 存储端口驱动程序创建自己的功能设备对象 (FDO) 。 USB 存储端口驱动程序可以将物理存储设备分为多达16个逻辑单元。 在图所示的示例中，USB 存储设备包含袖珍闪存设备和智能媒体设备的单独槽。 因此，在此示例中，USB 存储端口驱动程序创建两个单独的 PDOs，一个用于 Compact 闪存设备，另一个用于智能媒体设备。

4.  USB 存储端口驱动程序上面的堆栈按本机磁盘类驱动程序的常用方式进行管理。 Disk 类驱动程序为磁盘创建一个 PDO 和 FDO 作为一个整体 (分区零) ，并为磁盘上的每个分区创建 PDOs。

5.  分区管理器为每个磁盘分区创建一个 FDO。

 

 




