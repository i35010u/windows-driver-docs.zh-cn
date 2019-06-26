---
title: NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG
description: 微型端口驱动程序使用 NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 状态指示通知 NDIS 和基础驱动程序已被微型端口适配器在标头数据拆分配置中的更改。
ms.assetid: 6605d888-bcbe-4898-aa25-4a4352fc50de
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_HD_SPLIT_CURRENT_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b22e475563ab4a6ec4325d66e02655707cbc54bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368590"
---
# <a name="ndisstatushdsplitcurrentconfig"></a>NDIS\_状态\_HD\_拆分\_当前\_配置


微型端口驱动程序使用 NDIS\_状态\_HD\_拆分\_当前\_配置的配置状态指示通知 NDIS 和基础驱动程序已被更改标头数据拆分微型端口适配器。

<a name="remarks"></a>备注
-------

当微型端口驱动程序收到[OID\_代\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)集请求，该驱动程序必须使用的内容[ **NDIS\_HD\_拆分\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构，以更新当前的微型端口适配器配置。 更新后，微型端口驱动程序必须报告更改与的 NDIS\_状态\_HD\_拆分\_当前\_配置状态指示。 状态指示可确保所有基础驱动程序更新使用新的信息。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含[ **NDIS\_HD\_拆分\_当前\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)结构。 此结构指定微型端口适配器的当前标头数据拆分的配置。

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
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_HD\_拆分\_当前\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_hd_split_current_config)

[**NDIS\_状态\_HD\_拆分\_当前\_配置**](ndis-status-hd-split-current-config.md)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_HD\_拆分\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-hd-split-parameters)

 

 




