---
title: NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE
description: 支持 NDIS Service Service (QoS) 的微型端口驱动程序会在首次从对等端接收到其远程 NDIS QoS 参数时发出 NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 状态指示，或在以后更改。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f4e8b3d6ab6d92836dde1607b947bb6b2da33f6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801475"
---
# <a name="ndis_status_qos_remote_parameters_change"></a>NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改


支持 NDIS Service Service (QoS) 的微型端口驱动程序会在首次从对等端接收或更改其远程 NDIS QoS 参数时发出 **ndis \_ 状态 \_ QoS \_ 远程 \_ 参数 \_ 更改** 状态指示。 微型端口驱动程序通过 IEEE 802.1 Qaz 数据中心桥接 Exchange (DCBX) 协议从远程对等机接收这些 QoS 参数。

当微型端口驱动程序发出此状态指示时，它会将 [**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员设置为指向 [**ndis \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。 驱动程序用其远程 NDIS QoS 参数初始化此结构。

**注意**  此 NDIS 状态指示仅对支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

微型端口驱动程序使用 DCBX 协议接收远程对等方的 QoS 参数。 微型端口驱动程序基于其本地和远程 QoS 设置解析其操作的 NDIS QoS 参数。 解决操作参数后，微型端口驱动程序会将网络适配器配置为用于 QoS 数据包传输的这些参数。

有关驱动程序如何解析其操作 NDIS QoS 参数设置的详细信息，请参阅 [解决操作 Ndis qos](./resolving-operational-ndis-qos-parameters.md)参数。

微型端口驱动程序必须遵循以下准则，以发出 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示：

-   如果微型端口驱动程序尚未收到来自远程对等方的 DCBX 帧，则它不能发出 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示。

-   微型端口驱动程序必须在第一次从远程对等节点接收到 QoS 设置之后发出 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示。

    **注意**  如果在设置驱动程序的本地 QoS 参数之前，网络适配器接收到对等方的远程 QoS 参数设置，则微型端口驱动程序必须发出此状态指示。 有关详细信息，请参阅 [设置本地 NDIS QoS 参数](./setting-local-ndis-qos-parameters.md)。

     

-   在此初始状态指示后，微型端口驱动程序必须仅在确定远程对等机上 QoS 设置的更改时发出 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示。

    **注意**  如果没有对远程 NDIS QoS 参数的更改，微型端口驱动程序不得发出 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示。 如果驱动程序确实会导致此类状态指示，NDIS 可能不会将该指示传递到过量驱动程序。

     

**注意**  过量驱动程序可以使用 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示来确定远程 NDIS QOS 参数。 此外，这些驱动程序还可以发出 oid [ \_ qos \_ 远程 \_ 参数](./oid-qos-remote-parameters.md) 的 oid 查询请求，以随时获取远程 NDIS qos 参数。

 

有关微型端口驱动程序如何发出 **NDIS \_ 状态 \_ QOS \_ 远程 \_ 参数 \_ 更改** 状态指示的详细信息，请参阅 [指示对远程 NDIS QOS 参数所做的更改](./indicating-changes-to-the-remote-ndis-qos-parameters.md)。

有关远程 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](./overview-of-ndis-qos-parameters.md)"。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ QOS \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)

[OID \_ QOS \_ 远程 \_ 参数](./oid-qos-remote-parameters.md)

 

