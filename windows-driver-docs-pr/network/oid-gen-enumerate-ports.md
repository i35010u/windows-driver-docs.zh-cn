---
title: OID_GEN_ENUMERATE_PORTS
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_ENUMERATE_PORTS OID 来确定与基础微型端口适配器关联的活动 NDIS 端口的特征。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ENUMERATE_PORTS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: be243bdef2adf782a4a513981d926e2c14221eef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837113"
---
# <a name="oid_gen_enumerate_ports"></a>OID \_ 代 \_ 枚举 \_ 端口


作为查询，NDIS 和过量驱动程序使用 OID \_ 代 \_ 枚举 \_ 端口 oid 来确定与基础微型端口适配器关联的活动 NDIS 端口的特征。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 将返回 NDIS \_ 状态 \_ 成功，并提供 [**ndis \_ 端口 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array) 结构中的查询结果。 NDIS **NumberOfPorts** 端口数组的 NumberOfPorts \_ 成员 \_ 包含与微型端口适配器关联的活动端口数。 NDIS 端口数组的 **端口** 成员 \_ \_ 包含指向 [**ndis \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics) 结构的指针的列表。 每个 NDIS \_ 端口 \_ 特征结构定义单个 NDIDS 端口的特征。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 端口 \_ 数组**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)

[**NDIS \_ 端口 \_ 特征**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)

 

