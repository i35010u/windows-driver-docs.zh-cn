---
title: OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX
description: 作为一组 TCP/IP 传输使用 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX OID 请求微型端口驱动程序将指定的安全关联 (Sa) 添加到 nic。
ms.assetid: 9D356CFA-3353-4E62-9B1C-0FF650DCE75C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_TCP_TASK_IPSEC_OFFLOAD_V2_ADD_SA_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bd82ea83e066e7e5aaf1c468a4bab99f6cc01526
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569334"
---
# <a name="oidtcptaskipsecoffloadv2addsaex"></a>OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX


\[IPsec 任务卸载功能已弃用，不应使用。\]

作为一组 TCP/IP 传输使用 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_EX OID 以请求微型端口驱动程序添加指定的安全关联 (Sa) 到 nic。

**请注意**  NDIS 支持此 OID 与 direct 的 OID 请求接口。 有关直接 OID 请求接口的详细信息，请参阅[NDIS 6.1 直接 OID 请求接口](https://msdn.microsoft.com/library/windows/hardware/ff564736)。

 

<a name="remarks"></a>备注
-------

所有 NDIS 6.30 微型端口驱动程序支持 IPsec 都卸载版本 2 (IPsecOV2) 必须支持此 OID。

TCP/IP 传输确定 NIC 可以执行 IPsecOV2 操作后，TCP/IP 传输请求的微型端口驱动程序添加 SAs。 传输添加 SA 之前，传输不能卸载到 NIC IPsecOV2 操作。

微型端口驱动程序配置的 NIC IPsecOV2 对该 SAs 的处理。 成功设置为 OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA\_EX、 微型端口驱动程序提供标识的句柄卸载中的 SA **OffloadHandle**的成员[ **IPSEC\_卸载\_V2\_添加\_SA\_EX**](https://msdn.microsoft.com/library/windows/hardware/hh463943)结构。 （例如，传输使用句柄发送路径中以指示其卸载 SA 使用）。 如果已卸载的 SA，集请求是成功的。

微型端口驱动程序可以返回 OID 请求的失败状态，如当 NIC 不足的容量来卸载多个 SAs 时。 此外，微型端口驱动程序可能会返回故障状态，因为它需要避免争用条件。 在这种情况下，NIC 配置更改并不包括特定的算法。

如果请求失败，已不会卸载 SAs。 如果 sa 发生故障，应设置微型端口驱动程序**OffloadHandle**成员中相应的 IPSEC\_卸载\_V2\_添加\_SA\_EX 结构**NULL**。

微型端口驱动程序报告可以支持中的 NIC 的 SAs 的最大数目**SaOffloadCapacity**的成员[ **NDIS\_IPSEC\_卸载\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)在初始化过程中的结构。 如果有必要，请 TCP/IP 传输可以设置[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_删除\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)要请求的 OID微型端口驱动程序从 NIC 中删除 SA

此 OID 是以前版本中，实质上是相同[OID\_TCP\_任务\_IPSEC\_卸载\_V2\_添加\_SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)。 唯一的区别是更新后[ **IPSEC\_卸载\_V2\_添加\_SA\_EX** ](https://msdn.microsoft.com/library/windows/hardware/hh463943)结构。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IPSEC\_OFFLOAD\_V2\_ADD\_SA\_EX**](https://msdn.microsoft.com/library/windows/hardware/hh463943)

[**NDIS\_IPSEC\_OFFLOAD\_V2**](https://msdn.microsoft.com/library/windows/hardware/ff565808)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_ADD\_SA](oid-tcp-task-ipsec-offload-v2-add-sa.md)

[OID\_TCP\_TASK\_IPSEC\_OFFLOAD\_V2\_DELETE\_SA](oid-tcp-task-ipsec-offload-v2-delete-sa.md)

 

 




