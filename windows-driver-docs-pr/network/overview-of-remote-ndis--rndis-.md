---
title: 远程 NDIS (RNDIS) 概述
description: 远程 NDIS (RNDIS) 概述
ms.assetid: 03da539d-9613-4454-8f79-514e76767af6
keywords:
- 远程 NDIS WDK 网络，体系结构
- 远程 NDIS WDK 网络，USB 传输
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 867803d43f142127c3bab565b28f5e53fdf11f73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843723"
---
# <a name="overview-of-remote-ndis-rndis"></a>远程 NDIS (RNDIS) 概述





远程 NDIS （RNDIS）无需硬件供应商为连接到 USB 总线的网络设备写入 NDIS 微型端口设备驱动程序。 远程 NDIS 通过定义与总线无关的消息集来完成此操作，并说明此消息集如何在 USB 总线上操作。 由于此远程 NDIS 接口已标准化，因此一组主机驱动程序可以支持连接到 USB 总线的任意数量的网络设备。 这极大地减少了设备制造商的开发负担，提高了系统的总体稳定性，因为无需新的驱动程序，而且还可以改善最终用户体验，因为没有要安装的驱动程序来支持新的 USB连接到总线的网络设备。 目前，Microsoft Windows 提供对远程 NDIS over USB 的支持。

下图显示了如何使用远程 NDIS 微型端口驱动程序和 USB 传输驱动程序的组合替换设备制造商的 NDIS 小型端口。 因此，设备制造商可以专注于设备实现，而无需开发 Windows NDIS 设备驱动程序。

![演示远程 ndis 体系结构的示意图](images/remote-ndis-architecture.png)

Microsoft 提供了 NDIS 微型端口驱动程序 Rndismp，该驱动程序实现了远程 NDIS 消息集并与通用总线传输驱动程序通信，后者又与相应的总线驱动程序通信。 此 NDIS 微型端口驱动程序由 Microsoft 实现和维护，并作为 Windows 的一部分进行分发。

以下远程 NDIS 消息集反映了 NDIS 微型端口驱动程序接口的语义：

-   初始化、重置和停止设备操作

-   传输和接收网络数据包

-   设置和查询设备操作参数

-   指示媒体链接状态和监视设备状态

Microsoft 还提供了一个 USB 总线传输驱动程序，该驱动程序实现了一种机制，用于在 USB 总线上传输远程 NDIS 消息。 此驱动程序传输远程 NDIS 微型端口驱动程序和特定于总线的驱动程序（如 USB）之间的标准化远程 NDIS 消息。 还需要特定于总线的驱动程序将任何特定于总线的要求（如电源管理）映射到标准远程 NDIS 消息。 USB 1.1 和2.0 的传输驱动程序由 Microsoft 实现和维护，并作为 Windows 的一部分进行分发。

此结构允许将单个设备驱动程序用于具有特定于总线的传输层的任何远程 NDIS 设备。 此外，特定总线上的所有网络设备只需要一个总线传输层。

本部分包括以下其他主题：

[远程 NDIS 的优点](benefits-of-remote-ndis.md)

[远程 NDIS 概念和定义](remote-ndis-concepts-and-definitions.md)

[远程 NDIS 文件命名约定](remote-ndis-file-naming-conventions.md)

[远程 NDIS 消息传递](remote-ndis-messaging.md)

[远程 NDIS 设备控制](remote-ndis-device-control.md)

[远程 NDIS INF 模板](remote-ndis-inf-template.md)

[远程 NDIS 设备的类型](types-of-remote-ndis-devices.md)

## <a name="related-topics"></a>相关主题


[Windows 中包含的 USB 类驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

 

 






