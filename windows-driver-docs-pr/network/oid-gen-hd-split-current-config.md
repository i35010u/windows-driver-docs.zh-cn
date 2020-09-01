---
title: OID_GEN_HD_SPLIT_CURRENT_CONFIG
description: 作为查询，过量驱动程序或管理实用工具可以使用 OID_GEN_HD_SPLIT_CURRENT_CONFIG OID 来确定微型端口适配器的当前标头数据拆分配置。
ms.assetid: fc363227-1040-45bc-8c76-2ac61606d777
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_HD_SPLIT_CURRENT_CONFIG 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b5d9f6dec2cbf0bca77fe5856431a062a50d93c4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208657"
---
# <a name="oid_gen_hd_split_current_config"></a>OID \_ GEN \_ HD \_ SPLIT \_ 当前 \_ 配置


作为查询，过量驱动程序或管理实用程序可以使用 OID \_ GEN \_ HD \_ SPLIT \_ 当前 \_ 配置 OID 来确定微型端口适配器的当前标头数据拆分配置。 系统管理员可以通过 WMI 接口使用与此 OID 关联的 GUID。

<a name="remarks"></a>备注
-------

NDIS 代表微型端口驱动程序处理此 OID。 NDIS 基于微型端口驱动程序初始化属性和 [**NDIS \_ 状态 \_ 高清 \_ 拆分 \_ 当前 \_ 配置**](./ndis-status-hd-split-current-config.md) 状态指示，来维护当前的标头数据拆分配置信息。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[**ndis \_ HD \_ SPLIT \_ 当前 \_ 配置**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。

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
<td><p>在 NDIS 6.1 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ HD \_ SPLIT \_ 当前 \_ 配置**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 状态 \_ HD \_ SPLIT \_ 当前 \_ 配置**](./ndis-status-hd-split-current-config.md)

 

