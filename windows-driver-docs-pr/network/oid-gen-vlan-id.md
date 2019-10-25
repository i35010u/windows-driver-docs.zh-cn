---
title: OID_GEN_VLAN_ID
description: 作为查询，OID_GEN_VLAN_ID OID 报告 NIC 的已配置 VLAN 标识符（ID）。
ms.assetid: 4e024951-a578-4f69-873d-879aecc96e68
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_VLAN_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b2c4eb1bc61af459abdb79eeab86f6635fee5a27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844592"
---
# <a name="oid_gen_vlan_id"></a>OID\_GEN\_VLAN\_ID


作为查询，OID\_代\_VLAN\_ID OID 报告 NIC 的配置 VLAN 标识符（ID）。

作为集，OID\_GEN\_VLAN\_ID OID 为微型端口驱动程序处理的 NIC 指定配置的 VLAN 标识符（ID）。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

传入此请求的信息缓冲区包含 NDIS\_VLAN\_ID 数据类型。 此 NDIS\_VLAN\_ID 值包含每个 IEEE 802.1 Q-2005 标准12个最低有效位的 VLAN ID。 NDIS\_VLAN\_ID 值的高序位保留，并且必须设置为0。 请注意，NDIS 将 NDIS\_VLAN\_ID 定义为 ULONG。

当传输使用 OID\_GEN\_VLAN\_ID 时，微型端口驱动程序将返回 NIC 的当前配置 VLAN ID。 当在集中使用时，微型端口驱动程序将 NIC 的当前配置 VLAN ID 设置为指定值。

在微型端口驱动程序的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数用于特定 NIC 时，驱动程序最初将 NIC 的 VLAN ID 设置为零。 然后，驱动程序的*MiniportInitializeEx*函数从注册表读取以下配置参数，如果该参数存在，则将 NIC 的 VLAN ID 设置为参数的值。

```syntax
VlanId, REG_DWORD
```

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


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

 

 




