---
title: 如何为 USB 设备分配容器 ID
description: 如何为 USB 设备分配容器 ID
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 439ad4dcf03fa994c92fd7c0cd3817b1a32baee8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828635"
---
# <a name="how-usb-devices-are-assigned-container-ids"></a>如何为 USB 设备分配容器 ID


对于通过通用串行总线 (USB) 连接到计算机的设备，以下流程图显示了用于将容器 ID 分配到 USB 设备节点的启发式 (*devnode*) 。

![说明 usb devnodes 的容器 id 试探法的流程图](images/containerid-6.png)

此试探法使用来自多个来源的信息来确定是否有以下有关 USB devnode 的情况：

-   Devnode 是否表示 USB 总线上的新设备？ 如果为 true，则 devnode 将接收到新的容器 ID。

-   Devnode 是否为现有设备的子 devnode？ 如果为 true，则 devnode 将继承父 devnode 的容器 ID。

USB 设备的容器 ID 通过多种方式生成。 此决定基于设备中包含的信息。 此信息是从 ACPI 设置、USB 总线驱动程序和 USB 集线器检索的。

此试探法针对即插即用 (PnP) manager 在 USB 总线上枚举的每个 devnode 执行这些步骤。

1.  当 USB 总线驱动程序查询时，USB 设备可以通过 Microsoft 操作系统 (OS) **ContainerID** 描述符报告容器 ID。

    从 Windows 7 开始，操作系统支持 Microsoft 操作系统 **ContainerID** 描述符。 通过此描述符，独立硬件供应商 (IHV) 可以准确指定设备的容器 ID。 因此，设备的容器 ID 是唯一的，不会在设备安装到的每台计算机上更改。 此外，如果它报告了 Microsoft 操作系统 **ContainerID** 描述符，则设备向操作系统指示所有枚举的 devnodes 都属于同一物理设备。

    Microsoft 操作系统 **ContainerID** 描述符旨在用于支持通过多个系统总线同时连接设备的设备。 例如，打印机可以通过使用 (Pnp-x) 即插即用扩展来支持同时进行的 USB 和 IP 网络连接。 通过使用单个 Microsoft 操作系统 **ContainerID** 描述符，在这两个传输上报告相同的容器 ID。 因此，PnP 管理器会确定每个总线枚举的 devnodes 是同一个物理设备的一部分。

    有关 Microsoft 操作系统 **ContainerID** 描述符的详细信息，请参阅 [microsoft os 描述符](/previous-versions/gg463179(v=msdn.10))。

2.  如果 USB 设备未报告 Microsoft 操作系统 **ContainerID** 描述符，则 usb 集线器驱动程序将查询 ACPI 以确定设备是否已连接到面向外部的端口。

    操作系统尝试查找 ACPI 地址 (**_ADR** 与设备连接到的 USB 端口的地址相匹配的) 对象。 如果找到匹配的地址对象，则操作系统将执行以下步骤：

    -   查询 (**_UPC**) 对象的 USB 端口功能，并选中 **PortIsConnectable** 值。 如果 **PortIsConnectable** 的值为非零值，则可以使用端口来连接外部设备。 因此，连接到此端口的任何设备都必须在计算机外部。

    -   如果计算机实现了 ACPI 3.0，并且 **PortIsConnectable** 字节为非零，则操作系统将另外查询物理位置说明 (**_PLD**) 对象。 操作系统检查是否在 **_PLD** 对象上设置了 **UserVisible** 位 (位 64) 。 它将执行此项检查以确保端口既可连接，又可在外部对用户可见。

    如果从 ACPI 收集的信息指示设备为外部设备，则 PnP 管理器将为设备生成容器 ID。 **ContainedID** 值可以是设备的 USB 序列号或随机生成的值的哈希值。 已为 devnode 分配此容器 ID。

    **注意**  如果操作系统确定设备在计算机内部运行，则 devnode 将继承父 devnode 的容器 ID，在这种情况下 (，) 是计算机本身的容器 ID。

     

3.  如果 ACPI 未返回与设备连接到的 USB 端口地址相匹配的 **_ADR** 对象，PnP 管理器将基于 devnode 的可移动状态生成容器 ID。

    USB 集线器驱动程序从中心查询 USB **RemoveAndPowerMask** 描述符，并检查是否为设备连接到的端口设置了 **DeviceRemovable** 位。 如果设置了 **DeviceRemovable** 位，则连接到该端口的设备将从中心可移动。 如果未设置 **DeviceRemovable** 位，则连接到该端口的设备将无法从中心移动。

    USB 总线驱动程序向 PnP 管理器报告端口可移动/非可移动状态，后者通过以下步骤为 devnode 生成 **ContainerId** ：

    -   如果集线器指示连接到给定端口的设备是从中心可移动的，则 PnP 管理器会确定连接到此端口的设备在计算机外部。 为 devnode 生成的容器 ID 是设备的 USB 序列号的哈希，或是随机生成的值。

    -   如果中心指示连接到给定端口的设备不能从集线器中移除，则 PnP 管理器会确定连接到此端口的设备是多功能设备的子功能。 在这种情况下，devnode 继承父 devnode 的容器 ID。

有关 ACPI 3.0 接口的详细信息，请参阅 [高级配置和电源接口规范修订版本 3.0 b](https://go.microsoft.com/fwlink/p/?linkid=145427)。

 

