---
title: OID_GEN_HD_SPLIT_PARAMETERS
description: 作为集，NDIS 和过量驱动程序或用户模式应用程序使用 OID_GEN_HD_SPLIT_PARAMETERS OID 来设置微型端口适配器的当前标头-数据拆分设置。
ms.assetid: 1b33c601-4302-4f63-8265-b75889b42d42
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_HD_SPLIT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a9d9387232d4ce872a64517758121a4691a46bf0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843020"
---
# <a name="oid_gen_hd_split_parameters"></a>OID\_GEN\_HD\_拆分\_参数


作为集，NDIS 和过量驱动程序或用户模式应用程序使用 OID\_GEN\_HD\_拆分\_参数 OID 来设置微型端口适配器的当前标头-数据拆分设置。 提供标头数据拆分服务的 NDIS 6.1 和更高的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

[**Ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含[**ndis\_HD\_SPLIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)结构。

在 NDIS 5 时，NDIS 可以将 OID\_GEN\_HD\_拆分\_参数 OID。*x*协议驱动程序绑定到 NDIS 6.1 微型端口。 NDIS 处理此 OID，然后将其传递给微型端口驱动程序，并更新微型端口适配器的 **\*HeaderDataSplit**标准化关键字（如果需要）。 如果禁用了标头-数据拆分，NDIS 不会将此 OID 发送到微型端口适配器。

只有在使用 NDIS\_HD\_SPLIT 启用了标头-数据拆分，\_在[**ndis\_hd\_split\_拆分中启用\_标头时，ndis 才会将此 OID 发送到微型端口驱动程序\_t_10_ 属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)结构。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_HD\_SPLIT\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_hd_split_attributes)

[**NDIS\_HD\_SPLIT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_hd_split_parameters)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




