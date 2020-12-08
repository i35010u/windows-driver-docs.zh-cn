---
title: OID_PD_QUERY_CURRENT_CONFIG
description: NDIS 协议或筛选器驱动程序将对象标识符 (OID) 方法请求 OID_PD_QUERY_CURRENT_CONFIG 发送到支持 PD 的微型端口驱动程序，以检索 PD 状态和功能。 所有支持 PD 的微型端口驱动程序都必须处理此 OID 请求。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PD_QUERY_CURRENT_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aa30ecd441bf37363d71cc05a969cea9334c3747
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815925"
---
# <a name="oid_pd_query_current_config"></a>OID \_ PD \_ 查询 \_ 当前 \_ 配置


NDIS 协议或筛选器驱动程序将对象标识符 (OID) 方法请求（oid \_ pd \_ 查询 \_ 当前 \_ 配置）发送到支持 pd 的微型端口驱动程序，以检索 pd 状态和功能。 所有支持 PD 的微型端口驱动程序都必须处理此 OID 请求。

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向缓冲区的指针。 此缓冲区包含以下数据：

-   [**NDIS \_ PD \_ CONFIG**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)结构

<a name="remarks"></a>备注
-------

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

[**NDIS \_ PD \_ CONFIG**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pd_config)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

