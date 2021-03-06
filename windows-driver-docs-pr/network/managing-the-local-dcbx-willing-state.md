---
title: 管理本地 DCBX 意愿状态
description: 管理本地 DCBX 意愿状态
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e472cd9d3addd4c8d904d443399ea1d06d82301
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248936"
---
# <a name="managing-the-local-dcbx-willing-state"></a>管理本地 DCBX 意愿状态


IEEE 802.1 Qaz 草案标准定义数据中心桥接 Exchange (DCBX) 协议。 此协议允许在网络适配器 (本地对等) 和直接连接的远程对等方之间交换 DCB 的配置参数。 这允许这些对等方调整和调整 Service (QoS) 参数的质量，以优化通过连接的数据传输。

根据本地和远程 QoS 参数设置，微型端口驱动程序可以解决冲突，并派生一组操作 QoS 参数。 网络适配器使用这些操作参数将数据包的优先级传输到远程对等方。 有关驱动程序如何解析其操作 NDIS QoS 参数设置的详细信息，请参阅 [解决操作 Ndis qos](resolving-operational-ndis-qos-parameters.md)参数。

DCBX 包含 DCB 类型- (TLV) 设置，这些设置通过链接层发现协议 (LLDP) 数据包上传输。 为以下类型的 QoS 参数定义单独的 TLV：

-   [增强的传输选择 (ETS)](enhanced-transmission-selection--ets--algorithm.md)

-   [基于优先级的流控制 (PFC)](priority-based-flow-control--pfc.md)

ETS 和 PFC 的 TLVs 定义了一个称为 " *愿意* 位" 的位。 如果网络适配器将其 TLV 设置发送到远程对等方，并将相应的位设置为1，则表示适配器愿意接受来自远程对等方的 QoS 参数。

设置这些 TLVs 中的个人愿意的能力取决于由微型端口驱动程序管理的本地 DCBX 的状态。 微型端口驱动程序必须遵循以下准则来管理本地 DCBX 适用的状态：

-   如果已禁用本地 DCBX，则在 DCBX TLVs 中必须将本地的相应位设置为零。 在这种情况下，始终从本地 QoS 参数解析操作 QoS 参数。 有关这些参数的详细信息，请参阅 [设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

-   如果启用了本地 DCBX "愿意" 状态，则必须在 DCBX TLVs 中将本地的 "愿意" 位设置为1。 在这种情况下，必须从远程 QoS 参数解析操作 QoS 参数。 有关这些参数的详细信息，请参阅 [接收远程 NDIS QoS 参数](receiving-remote-ndis-qos-parameters.md)。

    **注意**  如果启用了本地 DCBX，则微型端口驱动程序还可以根据独立硬件供应商 (IHV) 定义的任何专有 QoS 设置来解析其操作 QoS 参数。 对于不是由对等方进行远程配置或由操作系统本地配置的 QoS 参数，驱动程序只能执行此操作。

     

微型端口驱动程序按以下方式管理本地 DCBX 的状态：

-   当通过对 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数的调用来初始化微型端口驱动程序时，它应基于由 IHV 定义的专有 QoS 设置来启用 "适用于本地 DCBX" 的状态。

-   DCB 组件 (Msdcb.sys) 发出对象标识符 (OID) 方法请求 [oid \_ qos \_ 参数](./oid-qos-parameters.md) ，以在网络适配器上配置本地 QOS 参数。 此 OID 请求的 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。

    如果在此结构的 **Flags** 成员中设置了 "要识别的 **NDIS \_ QOS \_ 参数 \_** " 标志，则微型端口驱动程序将启用 DCBX。 如果未设置此位，微型端口驱动程序将禁用 DCBX。

有关 LLDP 的详细信息，请参阅 IEEE 802.1 AB-2005 标准。

有关本地 DCBX 适用于 bits 和 TLVs 的详细信息，请参阅 IEEE 802.1 Qaz 草案标准。

**注意** 从 Windows Server 2012 开始，可以通过 PowerShell cmdlet 配置 DCB 组件，以设置或清除在颁发 [OID \_ qos \_ 参数](./oid-qos-parameters.md)请求时的 **NDIS \_ qos \_ 参数 \_** （如果有）。 这会导致微型端口驱动程序分别启用或禁用本地 DCBX。

 

 

