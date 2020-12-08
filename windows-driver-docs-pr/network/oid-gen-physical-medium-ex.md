---
title: OID_GEN_PHYSICAL_MEDIUM_EX
description: 作为查询，OID_GEN_PHYSICAL_MEDIUM_EX OID 指定了微型端口适配器支持的物理介质的类型。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PHYSICAL_MEDIUM_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 04a265006fca9ecc3f47d4107380d293277230f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829455"
---
# <a name="oid_gen_physical_medium_ex"></a>OID \_ 代 \_ 物理 \_ 介质（ \_ EX）


作为查询，OID 代物理介质的使用 \_ \_ \_ \_ oid 指定了微型端口适配器支持的物理介质的类型。

<a name="remarks"></a>备注
-------

NDIS 处理 NDIS 6.0 和更高版本的小型小型驱动程序的此 OID。 微型端口驱动程序在初始化过程中提供了物理媒体值。

[**Ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含 ndis \_ 物理 \_ 媒体枚举值。

**注意**  OID 生成 \_ \_ 物理 \_ 媒体 \_ ex 和 [oid \_ 代 \_ 物理 \_ 介质](oid-gen-physical-medium.md) 之间的区别在于，Oid 生成 \_ \_ 物理 \_ 介质的 \_ 版本不会将 **NdisPhysicalMedium802 \_ 3** 类型重写为 **NdisPhysicalMediumUnspecified** ，而 oid \_ gen \_ 实地 \_ medium 仍会。 建议所有的1.x 驱动程序使用 EX 版本。 OID \_ 代 \_ 物理 \_ 介质（ \_ EX）通过 WMI GUID 公开。

 

微型端口驱动程序报告物理介质类型，以便将其物理介质与它们声明为 [支持的介质中 \_ \_ \_ ](oid-gen-media-supported.md) 的介质区分开来。

\_ \_ \_ \_ 对于支持较新网络的微型端口适配器，NDIS 支持 oid 第一代物理媒体（EX oid），即使这些网络将显示到操作系统中的数据包和作为标准的已知媒体类型。

较新的网络传输的数据包可能类似于标准介质，但可能具有新功能或与标准略有不同。 此 OID 存在，因此上层驱动程序和应用程序可以确定 NIC 连接到的实际网络。 检索有关基础网络的信息后，上层驱动程序和应用程序可以使用此信息来修改此类驱动程序和应用程序的行为方式。

若要清楚地区分 802.3 NIC 和未定义物理类型的仿真 802.3 NIC，NDIS 6.0 及更高版本和更高版本需要802.3 微型端口驱动程序来报告 **NdisPhysicalMedium802 \_ 3** 媒体类型。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见“备注”部分。）</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[支持 OID 生成 \_ \_ 媒体 \_](oid-gen-media-supported.md)

[OID \_ 代 \_ 物理 \_ 中型](oid-gen-physical-medium.md)

 

