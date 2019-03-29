---
title: OID_GEN_PHYSICAL_MEDIUM_EX
description: 为查询，OID_GEN_PHYSICAL_MEDIUM_EX OID 指定微型端口适配器支持的物理介质的类型。
ms.assetid: cbac8c9b-d7fe-4588-8a64-599d04a77a72
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PHYSICAL_MEDIUM_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0c0f0b934035cbe6cfac6e9f2cb82f6ee5efb277
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564607"
---
# <a name="oidgenphysicalmediumex"></a>OID\_GEN\_PHYSICAL\_MEDIUM\_EX


为查询，OID\_GEN\_物理\_MEDIUM\_EX OID 指定微型端口适配器支持的物理介质的类型。

<a name="remarks"></a>备注
-------

NDIS NDIS 6.0 和更高版本的微型端口驱动程序处理此 OID。 微型端口驱动程序在初始化期间提供的物理介质的值。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含 NDIS\_物理\_中等枚举值。

**请注意**  OID 之间的差异\_常规\_物理\_中等\_EX 和[OID\_常规\_物理\_介质](oid-gen-physical-medium.md)在于 OID\_代\_物理\_中等\_EX 版本中不重写**NdisPhysicalMedium802\_3** 与类型**NdisPhysicalMediumUnspecified**而 OID\_代\_物理\_中仍会执行。 我们建议 6.x 的所有驱动程序使用 EX 版本。 OID\_GEN\_物理\_MEDIUM\_EX 公开通过 WMI GUID。

 

微型端口驱动程序报告物理媒体类型以使其物理介质区别于声明它们中支持的媒体[OID\_代\_媒体\_支持](oid-gen-media-supported.md)OID 查询。

NDIS 支持 OID\_GEN\_物理\_MEDIUM\_EX OID 适用于支持较新的网络，即使这些网络传输到操作系统和与的 NDIS 的数据包的微型端口适配器标准的、 众所周知的媒体类型。

较新的网络传输的数据包，可能类似于标准介质，但可能包含新功能或从标准细微的差别。 此 OID 存在因此上层驱动程序和应用程序可以确定一个 NIC 连接到的实际网络。 检索有关基础网络的信息之后, 上层驱动程序和应用程序可以使用此信息来修改此类驱动程序和应用程序的行为方式。

为了清楚地区分 802.3 从为其是不存在定义的物理介质类型、 NDIS 6.0 和更高版本及更高版本的仿真 802.3 NIC 的 NIC 需要 802.3 微型端口驱动程序报告**NdisPhysicalMedium802\_3**媒体类型。

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
<td><p>支持 NDIS 6.20 及更高版本。 未请求的微型端口驱动程序。 （请参见备注部分。）</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[OID\_GEN\_媒体\_支持](oid-gen-media-supported.md)

[OID\_GEN\_PHYSICAL\_MEDIUM](oid-gen-physical-medium.md)

 

 




