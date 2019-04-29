---
title: NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE
description: 支持 NDIS 服务质量 (QoS) 的微型端口驱动程序发出 NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 状态指示其远程 NDIS QoS 参数既接收来自对等方第一次或更高版本更改时。
ms.assetid: 3DA5F4FA-193F-4716-8678-7B6FB833E68E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_QOS_REMOTE_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a281ceadb5bad5e45611603befa0fa553874ad1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362947"
---
# <a name="ndisstatusqosremoteparameterschange"></a>NDIS\_状态\_QOS\_远程\_参数\_更改


支持 NDIS 服务质量 (QoS) 问题的微型端口驱动程序**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示时其远程 NDIS QoS 参数既接收来自对等方第一次或更高版本更改。 微型端口驱动程序将从通过 IEEE 802.1Qaz 远程对等方接收这些 QoS 参数的数据中心桥接交换 (DCBX) 协议。

当微型端口驱动程序将此状态指示时，它会设置**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)为指向的结构[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。 该驱动程序初始化其远程 NDIS QoS 参数与此结构。

**请注意**  此 NDIS 状态指示是仅对支持 IEEE 802.1 数据中心桥接 (DCB) 接口的微型端口驱动程序有效。

 

<a name="remarks"></a>备注
-------

微型端口驱动程序使用 DCBX 协议接收的远程对等方的 QoS 参数。 微型端口驱动程序解析其操作的 NDIS QoS 参数基于其本地和远程 QoS 设置。 解决操作参数后，微型端口驱动程序使用 QoS 数据包传输这些参数配置的网络适配器。

有关驱动程序如何解决其操作的 NDIS QoS 参数设置的详细信息，请参阅[解析操作的 NDIS QoS 参数](https://msdn.microsoft.com/library/windows/hardware/hh440220)。

微型端口驱动程序必须遵循这些准则以颁发**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示：

-   如果微型端口驱动程序尚未收到来自远程对等方 DCBX 帧，它必须不颁发**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示。

-   微型端口驱动程序必须发出**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示后它首先接收来自的 QoS 设置远程对等方。

    **请注意**  微型端口驱动程序必须发出此状态指示，如果网络适配器从对等方收到远程 QoS 参数设置之前设置驱动程序的本地 QoS 参数。 有关详细信息，请参阅[设置本地 NDIS QoS 参数](https://msdn.microsoft.com/library/windows/hardware/hh440225)。

     

-   在此初始状态指示后, 微型端口驱动程序必须只能颁发**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示时它确定远程对等方上的 QoS 设置中的更改。

    **请注意**  微型端口驱动程序必须发出**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示如果有了对远程 NDIS QoS 参数的任何更改。 如果该驱动程序会使这种类型的状态指示，NDIS 不可能将指示传递给过量驱动程序。

     

**请注意**  过量驱动程序可以使用**NDIS\_状态\_QOS\_远程\_参数\_更改**会向状态指示确定远程 NDIS QoS 参数。 或者，这些驱动程序还可以颁发的 OID 查询请求[OID\_QOS\_远程\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451841)在任何时候获取远程 NDIS QoS 参数。

 

有关如何微型端口驱动程序问题的详细信息**NDIS\_状态\_QOS\_远程\_参数\_更改**状态指示，请参阅[指示对远程 NDIS QoS 参数更改](https://msdn.microsoft.com/library/windows/hardware/hh406724)。

有关远程 NDIS QoS 参数的详细信息，请参阅[NDIS QoS 参数的概述](https://msdn.microsoft.com/library/windows/hardware/hh440130)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)

[**NDIS\_QOS\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh451640)

[OID\_QOS\_远程\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451841)

 

 




