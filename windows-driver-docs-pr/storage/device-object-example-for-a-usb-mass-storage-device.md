---
title: USB 大容量存储设备的设备对象示例
description: USB 大容量存储设备的设备对象示例
ms.assetid: 402b99f2-a253-4a43-9c73-d3d2fd066c23
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
- USB 大容量存储设备示例 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32e55fa061397ef29909427bc8bd7c3581f015ba
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544236"
---
# <a name="device-object-example-for-a-usb-mass-storage-device"></a>USB 大容量存储设备的设备对象示例


## <span id="ddk_device_object_example_for_a_usb_mass_storage_device_kg"></span><span id="DDK_DEVICE_OBJECT_EXAMPLE_FOR_A_USB_MASS_STORAGE_DEVICE_KG"></span>


下图显示了为复合 USB 大容量存储设备包含智能媒体槽和 Compact Flash 槽创建设备对象。

![创建包含智能媒体槽和 Compact Flash 槽复合的 USB 大容量存储设备的设备对象](images/usbstor.png)

复合 USB 大容量存储设备的的设备的对象树

从图底部开始，以下列表描述每个设备对象或设备对象堆栈和其关联的驱动程序：

1.  PCI 总线驱动程序枚举 USB 主控制器。 系统加载端口驱动程序， *usbport.sys*，以及其随附的微型端口 （不在图中所示）。 然后， *usbport.sys*创建主控制器 FDO。

2.  端口驱动程序枚举在系统中，从根集线器的 USB 集线器。 *Usbhub.sys*驱动程序管理所有 USB 集线器。 该图仅显示一个级别中心的设备对象，但 USB 允许菊花链的中心的设备，因此可能会有许多的多个中心的设备对象树中。 中心驱动程序检测和枚举 USB 大容量存储设备并为其创建 PDO。

3.  Windows 提供 USB 存储端口驱动程序， *usbstor.sys*，可用作 USB 堆栈和本机 Windows 存储类驱动程序之间的接口。 USB 存储端口驱动程序创建其自己的功能的设备对象 (FDO)。 USB 存储端口驱动程序可以将物理存储设备划分为多达 16 个逻辑单元。 在图所示示例中，USB 存储设备包含单独插槽 Compact Flash 设备和智能的媒体设备。 因此，在此示例中，USB 存储端口驱动程序将创建两个单独 PDOs，另一个用于 Compact Flash 设备，另一个用于智能媒体设备。

4.  上的 USB 存储端口驱动程序的堆栈由本机磁盘类驱动程序管理以通常的方式。 磁盘类驱动程序的磁盘上创建一个 PDO 和作为一个整体 （分区零），磁盘 FDO 和 PDOs 为每个分区。

5.  分区管理器创建的每个磁盘分区 FDO。

 

 




