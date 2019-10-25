---
title: OID_GEN_PHYSICAL_MEDIUM_EX
description: 作为查询，OID_GEN_PHYSICAL_MEDIUM_EX OID 指定了微型端口适配器支持的物理介质的类型。
ms.assetid: cbac8c9b-d7fe-4588-8a64-599d04a77a72
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PHYSICAL_MEDIUM_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b808aeda7ac7383314f94a1e77b8535ea502843
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824385"
---
# <a name="oid_gen_physical_medium_ex"></a>OID\_代\_物理\_中型\_EX


作为查询，OID\_代\_物理\_中型\_EX OID 指定微型端口适配器支持的物理介质的类型。

<a name="remarks"></a>备注
-------

NDIS 处理 NDIS 6.0 和更高版本的小型小型驱动程序的此 OID。 微型端口驱动程序在初始化过程中提供了物理媒体值。

[ **\_OID 的 ndis\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员包含一个 NDIS\_物理\_中型枚举值。

**请注意**  OID\_GEN\_物理\_中型\_EX 和 OID 之间的差异\_[物理\_介质](oid-gen-physical-medium.md)\_t_13_ EX 版本不会将**NdisPhysicalMedium802\_3**类型重写为**NDISPHYSICALMEDIUMUNSPECIFIED** ，而 OID\_GEN\_物理\_中型仍会。 建议所有的1.x 驱动程序使用 EX 版本。 OID\_代\_物理\_中型\_例如通过 WMI GUID 公开。

 

微型端口驱动程序报告物理介质类型，以便将其物理介质与它们声明为支持在[OID\_GEN\_介质\_支持](oid-gen-media-supported.md)的 oid 查询的介质区分开来。

NDIS 支持 OID\_GEN\_物理\_中型\_EX OID，适用于支持较新网络的微型端口适配器，即使这些网络会将显示到操作系统和 NDIS 的数据包传输为标准、众所周知的媒体各种.

较新的网络传输的数据包可能类似于标准介质，但可能具有新功能或与标准略有不同。 此 OID 存在，因此上层驱动程序和应用程序可以确定 NIC 连接到的实际网络。 检索有关基础网络的信息后，上层驱动程序和应用程序可以使用此信息来修改此类驱动程序和应用程序的行为方式。

若要清楚地将 802.3 NIC 与未定义物理类型的仿真 802.3 NIC 区分开来，NDIS 6.0 及更高版本和更高版本需要802.3 微型端口驱动程序来报告**NdisPhysicalMedium802\_3**媒体类型。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见 "备注" 部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[支持 OID\_GEN\_介质\_](oid-gen-media-supported.md)

[OID\_GEN\_物理\_中型](oid-gen-physical-medium.md)

 

 




