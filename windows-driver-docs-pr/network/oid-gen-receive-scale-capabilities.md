---
title: OID_GEN_RECEIVE_SCALE_CAPABILITIES
description: 为查询，过量驱动程序可以使用 OID_GEN_RECEIVE_SCALE_CAPABILITIES OID 来查询接收方缩放 (RSS) 功能的 NIC 和其微型端口驱动程序。
ms.assetid: b7640ec3-248c-4db2-818d-3976df2dcb9b
ms.date: 08/08/2017
keywords: -OID_GEN_RECEIVE_SCALE_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3bd06464c699e3befb5f228fb637d7b326b0d936
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355127"
---
# <a name="oidgenreceivescalecapabilities"></a>OID\_GEN\_接收\_规模\_功能


为查询，过量驱动程序可以使用 OID\_GEN\_接收\_规模\_功能 OID 来查询接收方缩放 (RSS) 功能的 NIC 和其微型端口驱动程序。

<a name="remarks"></a>备注
-------

NDIS 微型端口驱动程序不会收到此 OID 请求。 NDIS 处理查询的微型端口驱动程序。

微型端口驱动程序返回中的 RSS 功能[ **NDIS\_接收\_规模\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)结构。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_接收\_规模\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_scale_capabilities)

 

 




