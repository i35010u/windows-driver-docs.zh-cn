---
title: 设备树
description: 设备树
ms.assetid: 3220389a-06cc-4a43-8164-b785d1a16365
keywords:
- devnodes WDK PnP
- nonpresent 设备 WDK
- PnP WDK 内核，设备树
- 即插即用 WDK 内核，设备树
- 删除关系 WDK PnP
- 弹出关系 WDK PnP
- 设备树 WDK PnP
- 树 WDK PnP
- 设备节点 WDK PnP
- 子设备 WDK PnP
- 层次结构 WDK PnP
- 关系 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1abe07ceafb37ea3bcffc2ee8272d992facb9caa
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184791"
---
# <a name="device-tree"></a>设备树





PnP 管理器维护一个设备树，该树跟踪系统中的设备。 下图显示了一个示例系统配置的设备树。

![示例 pnp 设备树](images/devtree.png)

设备树包含有关系统上的设备的信息。 在计算机启动时，PnP 管理器将生成此树，使用驱动程序和其他组件中的信息，在添加或删除设备时更新树。

设备树的每个节点称为设备节点或 *devnode*。 Devnode 由设备的驱动程序的 *设备对象* 以及系统维护的内部信息组成。 因此，每个 *设备堆栈*都有一个 devnode。

PnP 管理器使用 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md) 请求来请求总线驱动程序的子设备列表。 总线驱动程序根据其总线协议确定子项列表。 例如， [WINDOWS acpi 驱动程序](acpi-driver.md)Acpi.sys 在 ACPI 命名空间中查找，pci 驱动程序查询 pci 配置空间，usb 集线器驱动程序遵循 usb 总线协议。

设备树是分层的，总线上的设备表示为总线适配器、控制器或其他 *总线设备*的 "子级"。  (总线设备是指可以连接到其他物理、逻辑或虚拟设备的任何设备。 ) 你可以使用设备管理器在设备树中看到设备的层次结构，并选择允许你按连接查看设备的 "查看" 选项。

设备树的层次结构反映了计算机中附加设备的结构。 PnP 管理器在管理设备时使用此层次结构。 例如，如果用户请求将 USB 控制器从上图所表示的计算机中拔出，则 PnP 管理器会从设备树确定，此操作会导致其他三个设备 (USB 集线器、操纵杆和摄像机) 。 当 PnP 管理器查询 USB 控制器的驱动程序以确定是否可以安全地删除控制器时，它还会将控制器后代的驱动程序 (集线器、操纵杆和相机) 。

设备树是动态的。 在将设备添加到计算机并将其从计算机中删除时，PnP 管理器 (与驱动程序一起) 维护系统上的设备的当前图片。

除了设备树中表示的层次结构关系外，计算机上的设备还存在其他关系。 其中包括 *删除关系* 和 *弹出关系*。 有关详细信息，请参阅 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md) 的参考页。

不能对设备树的生成顺序作出任何假设，只是在它的任何子设备之前配置了总线设备。 例如，不应假定总线上的一个设备在总线上的另一个设备之前配置。

 

