---
title: 远程 NDIS (RNDIS) 的概述
description: 远程 NDIS (RNDIS) 的概述
ms.assetid: 03da539d-9613-4454-8f79-514e76767af6
keywords:
- 远程 NDIS WDK 网络、 体系结构
- 远程 NDIS WDK 网络、 USB 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfcc0748f952439cf1de6b2b8380a855f9d2b7b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541544"
---
# <a name="overview-of-remote-ndis-rndis"></a>远程 NDIS (RNDIS) 的概述





远程 NDIS (RNDIS) 不需要硬件供应商编写与 USB 总线连接的网络设备的 NDIS 微型端口设备驱动程序。 远程 NDIS 通过定义独立于总线的消息集和此消息集通过 USB 总线的运行方式的说明完成此操作。 由于此远程 NDIS 接口进行了标准化，一组主机驱动程序可以支持任意数量的网络连接到 USB 总线的设备。 这显著减少了设备制造商的开发负担，提高了系统的整体稳定性，因为没有新的驱动程序是必需的并改善最终用户体验，因为没有驱动程序安装以支持新的 USB总线连接的网络设备。 当前 Microsoft Windows 还提供了通过 USB 远程 ndis 支持。

下图显示了替换为设备制造商的 NDIS 微型端口与远程 NDIS 微型端口驱动程序和 USB 传输驱动程序的组合。 设备制造商可以因此专注于设备实现，而无需开发 Windows NDIS 设备驱动程序。

![说明的远程 ndis 体系结构的关系图](images/remote-ndis-architecture.png)

Microsoft 提供的 NDIS 微型端口驱动程序 Rndismp.sys，实现远程 NDIS 消息组并与泛型总线传输驱动程序，它又与其相应的总线驱动程序进行通信。 此 NDIS 微型端口驱动程序是实现并由 Microsoft 维护和作为 Windows 的一部分分发。

以下远程 NDIS 消息设置镜像 NDIS 微型端口驱动程序接口的语义：

-   初始化、 重置，以及停止设备操作

-   传输和接收网络数据包

-   设置和查询设备操作参数

-   表示媒体链接状态和监视设备状态

Microsoft 还提供了实现了一个机制用于通过 USB 总线执行远程 NDIS 消息 USB 总线传输驱动程序。 此驱动程序会将标准化远程 NDIS 消息总线特定于驱动程序，如 USB 远程 NDIS 微型端口驱动程序之间传输。 总线特定于驱动程序也需要将任何特定于总线的要求，如电源管理，为标准化远程 NDIS 消息映射。 USB 1.1 和 2.0 的传输驱动程序是实现并由 Microsoft 维护，作为 Windows 的一部分分发。

此结构使单个设备驱动程序以用于任何远程 NDIS 设备总线特定于传输层。 此外，只有一个总线传输层是适用于特定的总线上的所有网络设备必需的。

本部分包括以下其他主题：

[远程 NDIS 的优点](benefits-of-remote-ndis.md)

[远程 NDIS 概念和定义](remote-ndis-concepts-and-definitions.md)

[远程 NDIS 文件命名约定](remote-ndis-file-naming-conventions.md)

[远程 NDIS 消息传送](remote-ndis-messaging.md)

[远程 NDIS 设备控制](remote-ndis-device-control.md)

[远程 NDIS INF 模板](remote-ndis-inf-template.md)

[类型的远程 NDIS 设备](types-of-remote-ndis-devices.md)

## <a name="related-topics"></a>相关主题


[包含在 Windows 中的 USB 类驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff538820)

 

 






