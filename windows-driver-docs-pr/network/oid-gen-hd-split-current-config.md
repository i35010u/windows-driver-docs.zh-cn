---
title: OID_GEN_HD_SPLIT_CURRENT_CONFIG
description: 为查询，过量驱动程序或管理实用程序可用于 OID_GEN_HD_SPLIT_CURRENT_CONFIG OID 确定微型端口适配器的当前标头数据拆分配置。
ms.assetid: fc363227-1040-45bc-8c76-2ac61606d777
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_HD_SPLIT_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bffe555573f5809d975e41816bef8e0828d7a3ee
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369123"
---
# <a name="oidgenhdsplitcurrentconfig"></a>OID\_GEN\_HD\_拆分\_当前\_配置


为查询，过量驱动程序或管理实用程序可以使用 OID\_GEN\_HD\_拆分\_当前\_配置 OID 来确定当前的标头数据拆分的微型端口配置适配器。 系统管理员可以使用与此 OID 通过 WMI 接口相关联的 GUID。

<a name="remarks"></a>备注
-------

NDIS 代表微型端口驱动程序处理此 OID。 NDIS 维护当前的标头数据拆分基于微型端口驱动程序初始化属性的配置信息并[ **NDIS\_状态\_HD\_拆分\_当前\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)状态指示。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含[ **NDIS\_HD\_拆分\_当前\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。

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
<td><p>支持 NDIS 6.1 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_状态\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-hd-split-current-config)

 

 




