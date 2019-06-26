---
title: OID_GEN_MAX_LINK_SPEED
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_MAX_LINK_SPEED OID 来确定最大支持传输和接收的微型端口适配器链接速度。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAX_LINK_SPEED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1c23d18623989c565594fdefb44f25d452ab46b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369061"
---
# <a name="oidgenmaxlinkspeed"></a>OID\_GEN\_MAX\_LINK\_SPEED


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_最大\_链接\_速度 OID 来确定支持的最大传输和接收的微型端口适配器链接速度。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化期间提供的最大链接速度。

若要指定最大链接速度，设置**MaxXmitLinkSpeed**并**MaxRcvLinkSpeed**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)微型端口驱动程序将传递给结构[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。 如果微型端口驱动程序不支持此 OID，则驱动程序应返回 NDIS\_状态\_不\_受支持。 如果微型端口驱动程序支持此 OID，它将返回中的最大链路速度[ **NDIS\_链接\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_speed)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_LINK\_SPEED**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_speed)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)

 

 




