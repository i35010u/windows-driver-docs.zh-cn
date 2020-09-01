---
title: NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE
description: VM 网络适配器微型端口驱动程序会在网络适配器的端口上更新路由域配置时生成 NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 状态指示。
ms.assetid: 4F3916B6-F52D-4B99-8F1C-A4A5BA9B307B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a1fafe60b3083608a5e621fa5c72964038e2df2a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212369"
---
# <a name="ndis_status_isolation_parameters_change"></a>NDIS \_ 状态 \_ 隔离 \_ 参数 \_ 更改


VM 网络适配器微型端口驱动程序在网络适配器的端口上更新路由域配置时，将生成 **NDIS \_ 状态 \_ 隔离 \_ 参数 \_ 更改** 状态指示。 这会触发 TCP 层通过颁发 [oid \_ GEN \_ 隔离 \_ 参数](oid-gen-isolation-parameters.md) OID 来重新查询多租户配置。 此状态指示没有状态缓冲区。

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
<td><p>在 NDIS 6.40 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ 代 \_ 隔离 \_ 参数](oid-gen-isolation-parameters.md)

 

