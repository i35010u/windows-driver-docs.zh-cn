---
title: NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE
description: 每当路由域配置更新网络适配器的端口上时，VM 网络适配器微型端口驱动程序将生成 NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 状态指示。
ms.assetid: 4F3916B6-F52D-4B99-8F1C-A4A5BA9B307B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4759dbe9f9f82789ff0b4efecff6d2325846ac72
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368578"
---
# <a name="ndisstatusisolationparameterschange"></a>NDIS\_状态\_隔离\_参数\_更改


VM 网络适配器微型端口驱动程序将生成**NDIS\_状态\_隔离\_参数\_更改**状态指示每当路由域配置更新网络适配器的端口上。 这会触发重新发出查询的多租户配置的 TCP 层[OID\_代\_隔离\_参数](oid-gen-isolation-parameters.md)OID。 此状态指示没有状态缓冲区。

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
<td><p>支持 NDIS 6.40 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_GEN\_隔离\_参数](oid-gen-isolation-parameters.md)

 

 




