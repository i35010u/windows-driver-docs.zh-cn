---
title: OID_GEN_HD_SPLIT_CURRENT_CONFIG
description: 作为查询，过量驱动程序或管理实用工具可以使用 OID_GEN_HD_SPLIT_CURRENT_CONFIG OID 来确定微型端口适配器的当前标头数据拆分配置。
ms.assetid: fc363227-1040-45bc-8c76-2ac61606d777
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_HD_SPLIT_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f9b0fac8398f0f6d05023b94b97e4c0cd0a88384
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843021"
---
# <a name="oid_gen_hd_split_current_config"></a>OID\_GEN\_HD\_拆分\_当前\_配置


作为查询，过量驱动程序或管理实用工具可以使用 OID\_GEN\_HD\_拆分\_当前\_配置 OID 来确定微型端口适配器的当前标头数据拆分配置。 系统管理员可以通过 WMI 接口使用与此 OID 关联的 GUID。

<a name="remarks"></a>备注
-------

NDIS 代表微型端口驱动程序处理此 OID。 NDIS 根据微型端口驱动程序初始化属性和[**ndis\_状态\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示，来维护当前的标头数据拆分配置信息。

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[**ndis\_HD\_SPLIT\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_HD\_SPLIT\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_状态\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)

 

 




