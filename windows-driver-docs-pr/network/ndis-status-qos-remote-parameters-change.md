---
title: NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE
description: 当首次从对等机接收到或稍后更改时，支持 NDIS 服务质量（QoS）的微型端口驱动程序会发出 NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 状态指示。
ms.assetid: 3DA5F4FA-193F-4716-8678-7B6FB833E68E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 80746117e4c132f9af3598438a4c273f11dbbf48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843528"
---
# <a name="ndis_status_qos_remote_parameters_change"></a>NDIS\_状态\_QOS\_远程\_参数\_更改


支持 NDIS 服务质量（QoS）的微型端口驱动程序会在 **\_QoS\_远程\_参数时发出 ndis\_状态，\_** 在对等方收到其远程 NDIS QoS 参数时，更改状态指示第一次或以后更改。 微型端口驱动程序通过 IEEE 802.1 Qaz 数据中心桥接交换（DCBX）协议从远程对等机接收这些 QoS 参数。

当微型端口驱动程序发出此状态指示时，它会将[**ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员设置为指向[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的指针。 驱动程序用其远程 NDIS QoS 参数初始化此结构。

**请注意**  此 NDIS 状态指示仅对支持 IEEE 802.1 数据中心桥接（DCB）接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

微型端口驱动程序使用 DCBX 协议接收远程对等方的 QoS 参数。 微型端口驱动程序基于其本地和远程 QoS 设置解析其操作的 NDIS QoS 参数。 解决操作参数后，微型端口驱动程序会将网络适配器配置为用于 QoS 数据包传输的这些参数。

有关驱动程序如何解析其操作 NDIS QoS 参数设置的详细信息，请参阅[解决操作 Ndis qos](https://docs.microsoft.com/windows-hardware/drivers/network/resolving-operational-ndis-qos-parameters)参数。

微型端口驱动程序必须遵循以下指导原则，使**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示：

-   如果微型端口驱动程序尚未收到来自远程对等方的 DCBX 帧，则它不能 **\_状态\_QOS\_远程\_参数\_更改**状态指示。

-   小型端口驱动程序必须在从远程对等节点首次接收到 QoS 设置后，将**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示。

    **请注意**  微型端口驱动程序必须在设置了驱动程序的本地 qos 参数之前从对等端接收远程 qos 参数设置后发出此状态指示。 有关详细信息，请参阅[设置本地 NDIS QoS 参数](https://docs.microsoft.com/windows-hardware/drivers/network/setting-local-ndis-qos-parameters)。

     

-   在此初始状态指示后，微型端口驱动程序必须仅 **\_QOS\_远程\_\_参数时发出 NDIS\_状态**，这会确定远程对等机上 QOS 设置的更改。

    **请注意**，  微型端口驱动程序不得将**NDIS\_状态\_QOS\_远程\_参数**，如果不存在对远程 NDIS QOS 参数的更改，则\_更改状态指示。 如果驱动程序确实会导致此类状态指示，NDIS 可能不会将该指示传递到过量驱动程序。

     

**请注意**  过量驱动程序可以使用**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示来确定远程 NDIS QOS 参数。 此外，这些驱动程序还可以发出 oid\_QOS 查询请求， [\_远程\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)随时获取远程 NDIS QOS 参数。

 

有关微型端口驱动程序如何发出**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示的详细信息，请参阅[指示对远程 NDIS QOS 参数所做的更改](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-changes-to-the-remote-ndis-qos-parameters)。

有关远程 NDIS QoS 参数的详细信息，请参阅 " [Ndis Qos 参数概述](https://docs.microsoft.com/windows-hardware/drivers/network/overview-of-ndis-qos-parameters)"。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)

[OID\_QOS\_远程\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-remote-parameters)

 

 




