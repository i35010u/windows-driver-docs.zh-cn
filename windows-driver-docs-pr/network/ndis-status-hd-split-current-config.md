---
title: NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 状态指示通知 NDIS 和过量驱动程序已更改了微型端口适配器的标头-数据拆分配置。
ms.assetid: 6605d888-bcbe-4898-aa25-4a4352fc50de
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e4a0b127ad71a6fe1d3928f7e7d779574b1bc077
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833742"
---
# <a name="ndis_status_hd_split_current_config"></a>NDIS\_状态\_HD\_拆分\_当前\_配置


微型端口驱动程序使用 NDIS\_状态\_HD\_拆分\_当前\_配置状态指示，以通知 NDIS 和过量驱动程序已更改了小型端口适配器的标头数据拆分配置。

<a name="remarks"></a>备注
-------

当微型端口驱动程序接收[OID\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)设置的请求时，驱动程序必须使用 NDIS\_[**HD\_split\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构的内容来更新当前小型端口适配器的配置。 更新完成后，微型端口驱动程序必须将 NDIS\_状态\_HD\_拆分\_当前\_配置状态指示报告更改。 状态指示可确保所有的过量驱动程序都用新信息更新。

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis\_HD\_SPLIT\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。 此结构指定微型端口适配器的当前标头-数据拆分配置。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_HD\_SPLIT\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_状态\_HD\_拆分\_当前\_配置**](ndis-status-hd-split-current-config.md)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)

 

 




