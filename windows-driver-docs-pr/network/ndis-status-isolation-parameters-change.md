---
title: NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE
description: VM 网络适配器微型端口驱动程序在网络适配器的端口上更新路由域配置时，会生成 NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 状态指示。
ms.assetid: 4F3916B6-F52D-4B99-8F1C-A4A5BA9B307B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_ISOLATION_PARAMETERS_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3fc7b46042a1d66b2fa4af28095f0cf378bbc8ec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844209"
---
# <a name="ndis_status_isolation_parameters_change"></a>NDIS\_状态\_隔离\_参数\_更改


VM 网络适配器微型端口驱动程序会在网络适配器的端口上更新路由域配置时，生成一个**NDIS\_状态\_隔离\_参数\_更改**状态指示。 这会触发 TCP 层通过[\_代\_隔离\_参数](oid-gen-isolation-parameters.md)OID 发出 oid 来重新查询多租户配置。 此状态指示没有状态缓冲区。

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
[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_代\_隔离\_参数](oid-gen-isolation-parameters.md)

 

 




