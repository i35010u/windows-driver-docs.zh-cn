---
title: OID_GEN_MAX_LINK_SPEED
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_MAX_LINK_SPEED OID 来确定微型端口适配器支持的最大传输和接收链接速度。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAX_LINK_SPEED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a0a6b8c7aebdddbd8617acbe05b52f7c367ff5ff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843067"
---
# <a name="oid_gen_max_link_speed"></a>OID\_代\_MAX\_链接\_速度


作为查询，NDIS 和过量驱动程序使用 OID\_代\_MAX\_LINK\_速度 OID 来确定微型端口适配器支持的最大传输和接收链接速度。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

小型端口驱动程序在初始化期间提供最大链接速度。

若要指定最大链接速度，请将[**NDIS\_微型端口\_\_\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的**MaxXmitLinkSpeed**和**MaxRcvLinkSpeed**成员设置为微型端口驱动程序传递给[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。 如果微型端口驱动程序不支持此 OID，驱动程序将返回 NDIS\_状态\_不\_支持。 如果微型端口驱动程序支持此 OID，它将返回[**NDIS\_链接\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed)结构的最大链接速度。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_链接\_速度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

 

 




