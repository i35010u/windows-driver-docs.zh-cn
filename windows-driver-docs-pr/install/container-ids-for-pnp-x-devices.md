---
title: PnP-X 设备的容器 ID
description: PnP-X 设备的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f496f74c0dec67b814ef35f50921f43930975603
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782953"
---
# <a name="container-ids-for-pnp-x-devices"></a>PnP-X 设备的容器 ID


PnP 扩展 (Pnp-x) 将 Windows 即插即用 (PnP) 扩展为支持通过基于 IP 的网络连接到计算机的设备。 有关 Pnp-x 的详细信息，请参阅 [pnp-x： Windows 规范即插即用扩展。](https://go.microsoft.com/fwlink/p/?linkid=142398                  )

Pnp-x 设备可指定容器 ID 作为其设备元数据中的 XML 元素。 支持两个协议：

-   Web 服务 (DPWS) 的设备配置文件。

    有关 DPWS 的详细信息，请参阅 [DPWS 规范。](https://go.microsoft.com/fwlink/p/?linkid=142400)

    有关通过 DPWS 支持容器 Id 的详细信息，请参阅 [DPWS 设备的容器 id](container-ids-for-dpws-devices.md)。

-   通用 PnP (UPnP) 。

    有关详细信息，请参阅 [UPnP 设备体系结构规范。](https://go.microsoft.com/fwlink/p/?linkid=142402)

    有关通过 UPnP 支持容器 Id 的详细信息，请参阅 [Upnp 设备的容器 id](container-ids-for-upnp-devices.md)。

如果 Pnp-id 设备未在 DPWS 设备元数据或 UPnP 设备说明文档中指定容器 ID，则 PnP 管理器会通过特定于设备支持的协议的算法为设备生成容器 ID：

-   对于 DPWS 设备，生成的容器 ID 是从设备终结点引用地址 (EPR) 中的 GUID 创建的，或者是设备的 EPR (的 SHA-1 哈希，如果不是 GUID) 。

-   对于 UPnP 设备，生成的容器 ID 是设备的唯一设备名称 (UDN) 。

    **注意**  在 Windows 10 中，PnP 管理器将始终使用上述算法生成 DPWS 设备的容器 ID，即使已在设备元数据中指定容器 ID 也是如此。

     

对于在单个总线或 Pnp-x 协议上操作的设备，即 Pnp-x 生成的容器 ID 就已足够。

多协议设备可能需要指定容器 ID。 在多协议设备中，将在每个协议上共享相同的容器 ID，以允许 Windows 将设备的所有实例组合成一个设备容器。 通过这种方式，可以通过 DPWS 和 UPnP 指定设备的容器 ID。

 

 





