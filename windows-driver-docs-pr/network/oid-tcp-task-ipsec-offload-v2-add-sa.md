---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA
description: 作为一组 TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA OID 请求微型端口驱动程序将指定的安全关联 (Sa) 添加到 nic。
ms.assetid: bd1d0cf2-234d-4c06-904e-fe2de6022981
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 35e3eb0253b8e671fc02efec29ba7363c7e1fa10
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350913"
---
# <a name="oidtcptaskipsecoffloadv2addsa"></a>OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组 TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA OID 以请求微型端口驱动程序添加指定的安全性关联 (Sa) 到 nic。

**请注意**  NDIS 支持此 OID 与 direct 的 OID 请求接口。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 OID 请求接口](https://msdn.microsoft.com/library/windows/hardware/ff564736)。

 

**请注意**  NDIS 6.1 和 6.20 中支持此 OID。 NDIS 6.30 和更高版本的驱动程序，请参阅[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)。

 

<a name="remarks"></a>备注
-------

所有 NDIS 6.1 和 6.20 微型端口驱动程序支持 IPsec 都卸载版本 2 (IPsecOV2) 必须支持此 OID。

TCP/IP 传输确定 NIC 可以执行 IPsecOV2 操作后，TCP/IP 传输请求的微型端口驱动程序添加 SAs。 传输添加 SA 之前，传输不能卸载到 NIC IPsecOV2 操作。

微型端口驱动程序收到[ **IPSEC\_卸载\_V2\_添加\_SA** ](https://msdn.microsoft.com/library/windows/hardware/ff556977)结构，其中包含指向下一步 IPSEC\_卸载\_V2\_添加\_SA 结构链接列表中的。 微型端口驱动程序配置的 NIC IPsecOV2 对该 SAs 的处理。 成功设置为 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA，微型端口驱动程序提供标识中卸载的 SAs 的句柄**OffloadHandle** IPSEC 成员\_卸载\_V2\_添加\_SA。 （例如，传输使用句柄发送路径中以指示其卸载 SA 使用）。 如果链接列表中的任何的 SAs 已卸载，集请求是成功的。

微型端口驱动程序可以返回 OID 请求的失败状态，如当 NIC 不足的容量来卸载多个 SAs 时。 此外，微型端口驱动程序可能会返回故障状态，因为它需要避免争用条件。 在这种情况下，NIC 配置更改并不包括特定的算法。

如果请求失败，已卸载无链接列表中的 SAs。 如果链接列表中特定 sa 发生故障，应设置微型端口驱动程序**OffloadHandle**成员中相应的 IPSEC\_卸载\_V2\_添加\_SA结构**NULL**。

微型端口驱动程序报告可以支持中的 NIC 的 SAs 的最大数目**SaOffloadCapacity**的成员[ **NDIS\_IPSEC\_卸载\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)在初始化过程中的结构。 如果有必要，请 TCP/IP 传输可以设置[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)要请求的 OID微型端口驱动程序从 NIC 中删除 SA

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
<td><p>在 NDIS 6.1 和 6.20 中受支持。 NDIS 6.30 和更高版本，使用<a href="oid-tcp-task-ipsec-offload-v2-add-sa-ex.md" data-raw-source="[OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)">OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX</a>。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IPSEC\_OFFLOAD\_V2\_ADD\_SA**](https://msdn.microsoft.com/library/windows/hardware/ff556977)

[**NDIS\_IPSEC\_OFFLOAD\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX](oid-tcp-task-ipsec-offload-v2-add-sa-ex.md)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




