---
title: PNP-X 的设备的容器 Id
description: PNP-X 的设备的容器 Id
ms.assetid: 6a1ea4e9-e672-4f37-ab26-932591fe4da4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1250b34309df64f25321c0e6154bdc0bb0032574
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519874"
---
# <a name="container-ids-for-pnp-x-devices"></a>PNP-X 的设备的容器 Id


即插即用扩展 (PNP-X) 通过基于 IP 的网络扩展了 Windows 即插即用和 Play (PnP)，以支持连接到计算机的设备。 有关 PNP-X 的详细信息，请参阅[PnP x:Windows 规范的即插扩展。](https://go.microsoft.com/fwlink/p/?linkid=142398                  )

PNP-X 的设备可在其设备元数据的 XML 元素形式指定一个容器 ID。 支持两种协议：

-   设备配置文件的 Web 服务 (DPWS)。

    DPWS 有关的详细信息，请参阅[DPWS 规范。](https://go.microsoft.com/fwlink/p/?linkid=142400)

    支持 DPWS 通过容器 Id 的详细信息，请参阅[DPWS 设备的容器 Id](container-ids-for-dpws-devices.md)。

-   通用即插即用 (UPnP)。

    有关详细信息，请参阅[UPnP 设备体系结构规范。](https://go.microsoft.com/fwlink/p/?linkid=142402)

    支持通过 UPnP 的容器 Id 的详细信息，请参阅[UPnP 设备的容器 Id](container-ids-for-upnp-devices.md)。

如果 PNP-X 的设备 DPWS 设备元数据或 UPnP 设备说明文档中未指定容器 ID，即插即用 manager 会生成特定于设备支持的协议的算法通过在设备的容器 ID:

-   对于 DPWS 设备生成的容器 ID 是从设备的终结点中的 GUID 创建引用 (EPR) 地址或设备的 EPR （如果不是一个 GUID） 的 sha-1 哈希。

-   对于 UPnP 设备，生成的容器 ID 是设备的唯一设备名称 (UDN)。

    **请注意**  在 Windows 10 中，即插即用管理器将始终生成 DPWS 设备的容器 ID 通过上述的算法，即使设备元数据中指定容器 ID。

     

对于单个总线或 PNP-X 的协议运行的设备，PNP-X 生成容器 ID 已足够。

多协议的设备可能想要指定的容器 id。 在多协议的设备，会在每个协议以允许进行分组的设备到一台设备的容器的所有实例的 Windows 上共享相同的容器 ID。 以这种方式，可以通过 DPWS 和 UPnP 指定设备的容器 ID。

 

 





