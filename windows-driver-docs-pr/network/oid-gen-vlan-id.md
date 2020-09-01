---
title: OID_GEN_VLAN_ID
description: 作为查询，OID_GEN_VLAN_ID OID (ID) 为 NIC 报告配置的 VLAN 标识符。
ms.assetid: 4e024951-a578-4f69-873d-879aecc96e68
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_VLAN_ID 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6f563c6bf01e6462b24d643fe485d92c132d5557
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206727"
---
# <a name="oid_gen_vlan_id"></a>OID \_ GEN \_ VLAN \_ ID


作为查询，OID \_ GEN \_ VLAN \_ ID oid 报告 NIC (ID) 配置的 vlan 标识符。

作为集，OID \_ GEN \_ VLAN \_ ID oid 为微型端口驱动程序处理的 NIC 指定配置的 VLAN 标识符 (ID) 。

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

此请求中传递的信息缓冲区包含 NDIS \_ VLAN \_ ID 数据类型。 此 NDIS \_ VLAN \_ id 值包含每个 IEEE 802.1 q-2005 标准中12个最低有效位的 VLAN id。 NDIS VLAN ID 值的更高顺序 \_ \_ 被保留，并且必须设置为0。 请注意，NDIS \_ 将 ndis VLAN \_ ID 定义为 ULONG。

当传输 \_ \_ 在查询中使用 OID GEN vlan \_ id 时，微型端口驱动程序将返回 NIC 的当前配置 vlan id。 当在集中使用时，微型端口驱动程序将 NIC 的当前配置 VLAN ID 设置为指定值。

在微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数用于特定 NIC 时，驱动程序最初将 NIC 的 VLAN ID 设置为零。 然后，驱动程序的 *MiniportInitializeEx* 函数从注册表读取以下配置参数，如果该参数存在，则将 NIC 的 VLAN ID 设置为参数的值。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)

 

