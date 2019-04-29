---
title: 如何为 USB 设备分配容器 ID
description: 如何为 USB 设备分配容器 ID
ms.assetid: 769f9486-d179-44f0-9fd1-b3e737143ced
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: a5298352c7941dba1511c0a5fe942b48cfde7992
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386972"
---
# <a name="how-usb-devices-are-assigned-container-ids"></a>如何为 USB 设备分配容器 ID


对于连接到计算机通过通用串行总线 (USB) 设备，下列流程图显示了用于将容器 ID 分配给 USB 设备节点的启发式方法 (*devnode*)。

![流程图，显示了 usb devnodes 容器 id 启发式方法](images/containerid-6.png)

此启发式方法使用从多个源的信息以确定是否满足有关 USB devnode 以下项之一：

-   Devnode 是否表示 USB 总线上的新设备？ 如果为 true，devnode 会收到一个新的容器 id。

-   是现有设备的子 devnode devnode？ 如果为 true，devnode 会继承父 devnode 的容器 ID。

以下几种方式生成 USB 设备的容器 ID。 此决定基于设备中包含的信息。 从 ACPI 设置、 USB 总线驱动程序和 USB 集线器检索此信息。

此启发式方法遵循 USB 总线上的插即用 (PnP) 管理器枚举每个 devnode 这些步骤。

1.  USB 设备通过 USB 总线驱动程序查询后，可以报告通过 Microsoft 操作系统 (OS) 的容器 ID **ContainerID**描述符。

    操作系统从 Windows 7 开始，支持 Microsoft 操作系统**ContainerID**描述符。 通过此说明符，独立硬件供应商 (IHV) 可以精确地指定设备的容器 ID。 因此，在安装设备的容器 ID 是唯一的不会更改每台计算机上的设备。 此外，如果报告 Microsoft OS **ContainerID**描述符，设备将指示对操作系统所有枚举的 devnodes 属于同一个物理设备。

    Microsoft OS **ContainerID**旨在使用在支持的多个系统总线通过在设备的同时连接的设备中的描述符。 例如，打印机可能使用插扩展 (PNP-X) 支持同时 USB 和 IP 网络连接。 通过使用单个 Microsoft OS **ContainerID**描述符，这两个传输报告 ID 相同的容器。 因此，即插即用管理器确定枚举每个总线 devnodes 属于同一个物理设备。

    有关 Microsoft 操作系统的详细信息**ContainerID**描述符，请参阅[Microsoft OS 描述符](https://go.microsoft.com/fwlink/p/?linkid=142397)。

2.  如果 USB 设备不报告 Microsoft OS **ContainerID**描述符，USB 集线器驱动程序查询 ACPI 来确定设备是否已附加到一个面向外部的端口。

    操作系统尝试查找 ACPI 地址 (**_ADR**) 与设备连接的 USB 端口的地址相匹配的对象。 如果找到匹配的地址对象，则操作系统将执行以下步骤：

    -   USB 端口功能 (**_UPC**) 对象查询并**PortIsConnectable**检查值。 如果**PortIsConnectable**具有非零值 0xff，可以使用该端口来连接外部设备。 因此，连接到此端口的任何设备必须是外部的计算机。

    -   如果在计算机实现 ACPI 3.0 和**PortIsConnectable**字节为非零值，操作系统将此外查询的物理位置描述 (**_PLD**) 对象。 如果操作系统会检查**UserVisible**位 （64 位） 上设置 **_PLD**对象。 这是作为额外检查以确保该端口可连接和外部对用户可见。

    如果从 ACPI 收集的信息指示外部设备，即插即用 manager 会生成设备的容器 ID。 **ContainedID**值是设备的 USB 序列号的哈希或随机生成的值。 Devnode 分配此容器 id。

    **请注意**  devnode 的操作系统决定是否在计算机的内部设备，如果将继承父 devnode，这是计算机本身的容器 ID （在这种情况下） 的容器 ID。

     

3.  如果未返回 ACPI **_ADR**与设备连接到 USB 端口地址相匹配的对象，即插即用管理器生成基于 devnode 可移动状态的容器 ID。

    USB 集线器驱动程序查询 USB **RemoveAndPowerMask**描述符从中心，并检查是否**DeviceRemovable**位设置为设备连接到端口。 如果**DeviceRemovable**设置位，连接到该端口的设备从中心可移动。 如果**DeviceRemovable**未设置位，连接到该端口的设备是 not 可移动从中心。

    USB 总线驱动程序向生成的即插即用管理器报告端口可移动/not-可移动状态**ContainerId**为 devnode 通过以下步骤：

    -   如果中心指示连接到给定的端口的设备从中心可移动，即插即用管理器确定设备附加到此端口是外部的计算机。 任一哈希的 USB 序列号的设备，则会生成 devnode 的容器 ID 或随机生成的值。

    -   如果中心指示，连接到给定的端口的设备不是从中心可移动，即插即用管理器确定设备附加到此端口是子功能的多功能设备。 在这种情况下，devnode 继承父 devnode 的容器 ID。

ACPI 3.0 接口的详细信息，请参阅[高级配置和电源接口规范修订 3.0b](https://go.microsoft.com/fwlink/p/?linkid=145427)。

 

 





