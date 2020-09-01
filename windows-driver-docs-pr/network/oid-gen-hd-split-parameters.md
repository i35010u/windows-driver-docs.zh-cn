---
title: OID_GEN_HD_SPLIT_PARAMETERS
description: 作为集，NDIS 和过量驱动程序或用户模式应用程序使用 OID_GEN_HD_SPLIT_PARAMETERS OID 设置微型端口适配器的当前标头-数据拆分设置。
ms.assetid: 1b33c601-4302-4f63-8265-b75889b42d42
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_HD_SPLIT_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4d1b286f49431bfc7fc1a7d6c52fc5cedea6f153
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208653"
---
# <a name="oid_gen_hd_split_parameters"></a>OID \_ GEN \_ HD \_ SPLIT \_ 参数


作为集，NDIS 和过量驱动程序或用户模式应用程序使用 OID \_ GEN \_ HD \_ SPLIT \_ PARAMETERS oid 设置微型端口适配器的当前标头-数据拆分设置。 提供标头数据拆分服务的 NDIS 6.1 和更高的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[**ndis \_ HD \_ SPLIT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构。

Ndis 5 时，NDIS 可能会设置 OID \_ GEN \_ HD \_ SPLIT \_ 参数 OID。*x* 协议驱动程序绑定到 NDIS 6.1 微型端口。 NDIS 处理此 OID，然后将其传递给微型端口驱动程序，并更新微型端口适配器的** \* HeaderDataSplit**标准化关键字（如果需要）。 如果禁用了标头-数据拆分，NDIS 不会将此 OID 发送到微型端口适配器。

仅当标头-数据拆分是通过使用 NDIS hd split 启用标头数据拆分来启用的，并且在 \_ \_ \_ \_ \_ \_ 微型端口初始化期间 [**NDIS \_ hd \_ 拆分 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes) 结构中，ndis 才会将此 OID 发送到微型端口驱动程序。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ HD \_ SPLIT \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)

[**NDIS \_ HD \_ SPLIT \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

