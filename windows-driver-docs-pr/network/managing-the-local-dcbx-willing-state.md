---
title: 管理本地 DCBX 愿意状态
description: 管理本地 DCBX 愿意状态
ms.assetid: B37CA18B-FCCD-414D-95AB-0C54B9F1F421
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8bf348dbc6ee033ae6cd0f0e3f85b04ff4bd7fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526398"
---
# <a name="managing-the-local-dcbx-willing-state"></a>管理本地 DCBX 愿意状态


IEEE 802.1Qaz 草稿标准定义的数据中心桥接交换 (DCBX) 协议。 此协议允许在网络适配器 （本地对等方） 和直接连接的远程对等方之间交换 DCB 配置参数。 这样，这些对等方可以调整和优化服务质量 (QoS) 参数，以优化通过连接的数据传输。

根据本地和远程 QoS 参数设置，微型端口驱动程序，解决这些冲突并派生一组操作的 QoS 参数。 网络适配器按优先顺序排列的远程对等方的数据包传输使用这些操作的参数。 有关驱动程序如何解决其操作的 NDIS QoS 参数设置的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

DCBX 包含结转链接层发现协议 (LLDP) 数据包的 DCB 类型-长度-值 (TLV) 设置。 单独 TLV 为以下类型的 QoS 参数定义：

-   [增强的传输选择 (ETS)](enhanced-transmission-selection--ets--algorithm.md)

-   [基于优先级的流控制 (PFC)](priority-based-flow-control--pfc.md)

ETS 和 PFC TLVs 定义有点称为*愿意*位。 如果网络适配器与愿意位设置为一个将其 TLV 设置发送到远程对等方，它表示适配器是愿意接受远程对等方的 QoS 参数。

在这些 TLVs 设置愿意的单个位的能力取决于本地 DCBX 愿意由微型端口驱动程序管理的状态。 微型端口驱动程序必须遵循以下准则，以便管理本地 DCBX 愿意状态：

-   如果禁用了本地 DCBX 愿意状态，则必须设置本地愿意位将注意力集中在 DCBX TLVs。 在这种情况下，从本地 QoS 参数始终解析得出的正常运行的 QoS 参数。 有关这些参数的详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

-   如果启用了本地 DCBX 愿意状态，则本地愿意位必须设置为一个 DCBX TLVs 中。 在这种情况下，必须从远程 QoS 参数解析操作的 QoS 参数。 有关这些参数的详细信息，请参阅[接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

    **请注意**  如果启用了本地 DCBX 愿意状态，微型端口驱动程序，也可以解决基于由独立硬件供应商 (IHV) 定义的任何专有 QoS 设置其操作的 QoS 参数。 该驱动程序可以仅执行此操作未配置远程对等方或本地操作系统的 QoS 参数。

     

微型端口驱动程序管理本地 DCBX 愿意状态如下所示：

-   通过调用初始化微型端口驱动程序时其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，则它应该启用本地 DCBX 愿意根据专有由 IHV 定义的 QoS 设置的状态.

-   DCB 组件 (Msdcb.sys) 发出的一个对象标识符 (OID) 方法请求[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)网络适配器上配置的本地 QoS 参数。 **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构为此 OID 请求包含一个指向[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。

    如果**NDIS\_QOS\_参数\_WILLING**中设置了标志**标志**此结构的成员，微型端口驱动程序，愿意状态 DCBX。 如果未设置此位，微型端口驱动程序禁用愿意状态 DCBX。

有关 LLDP 的详细信息，请参阅 IEEE 802.1AB-2005 标准。

有关本地 DCBX 愿意 bits 和 TLVs 的详细信息，请参阅 IEEE 802.1Qaz 草案标准。

**请注意**  从 Windows Server 2012 开始，DCB 配置该组件，可以通过 PowerShell cmdlet 来设置或清除**NDIS\_QOS\_参数\_WILLING**标志时它会发出[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)请求。 这将导致要分别启用或禁用本地 DCBX 愿意状态的微型端口驱动程序。

 

 

 





