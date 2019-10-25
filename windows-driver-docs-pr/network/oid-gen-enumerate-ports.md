---
title: OID_GEN_ENUMERATE_PORTS
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_ENUMERATE_PORTS OID 来确定与基础微型端口适配器关联的活动 NDIS 端口的特征。
ms.assetid: 42a12a05-e360-4493-b037-d3a63906a132
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_ENUMERATE_PORTS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 55dadb183b11c8574e1d46b145bf34e27d79facf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837983"
---
# <a name="oid_gen_enumerate_ports"></a>OID\_代\_枚举\_端口


作为查询，NDIS 和过量驱动程序使用 OID\_代\_枚举\_端口 OID 来确定与基础微型端口适配器关联的活动 NDIS 端口的特征。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 会将 NDIS\_状态恢复\_成功，并在[**NDIS\_端口\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)结构中提供查询的结果。 NDIS\_端口\_阵列的**NumberOfPorts**成员包含与微型端口适配器关联的活动端口数。 NDIS\_端口\_数组的**端口**成员包含指向[**NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)结构的指针的列表。 每个 NDIS\_端口\_特征结构定义单个 NDIDS 端口的特征。

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


[ **\_数组的 NDIS\_端口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_array)

[**NDIS\_端口\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_characteristics)

 

 




