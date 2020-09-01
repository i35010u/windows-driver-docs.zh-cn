---
title: NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 状态指示通知 NDIS 和过量驱动程序已更改了微型端口适配器的标头-数据拆分配置。
ms.assetid: 6605d888-bcbe-4898-aa25-4a4352fc50de
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bd7614d01c361d02afc3e4df8c62881c80457ebe
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212371"
---
# <a name="ndis_status_hd_split_current_config"></a>NDIS \_ 状态 \_ HD \_ SPLIT \_ 当前 \_ 配置


微型端口驱动程序使用 NDIS \_ 状态 \_ HD \_ SPLIT \_ 当前 \_ 配置状态指示通知 NDIS 和过量驱动程序已更改了微型端口适配器的标头数据拆分配置。

<a name="remarks"></a>备注
-------

当微型端口驱动程序收到 [OID 第一 \_ 代 \_ hd \_ split \_ 参数](./oid-gen-hd-split-parameters.md) set 请求时，驱动程序必须使用 [**NDIS \_ HD \_ split \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters) 结构的内容来更新微型端口适配器的当前配置。 更新后，微型端口驱动程序必须报告其 NDIS \_ 状态 \_ 高清 \_ 拆分 \_ 当前 \_ 配置状态指示的更改。 状态指示可确保所有的过量驱动程序都用新信息更新。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis \_ HD \_ SPLIT \_ 当前 \_ 配置**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。 此结构指定微型端口适配器的当前标头-数据拆分配置。

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
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ HD \_ SPLIT \_ 当前 \_ 配置**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS \_ 状态 \_ HD \_ SPLIT \_ 当前 \_ 配置**](ndis-status-hd-split-current-config.md)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ GEN \_ HD \_ SPLIT \_ 参数](./oid-gen-hd-split-parameters.md)

 

