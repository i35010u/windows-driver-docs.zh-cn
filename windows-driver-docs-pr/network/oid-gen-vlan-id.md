---
title: OID_GEN_VLAN_ID
description: 为查询，OID_GEN_VLAN_ID OID 报告配置的 VLAN 标识符 (ID) 的 nic。
ms.assetid: 4e024951-a578-4f69-873d-879aecc96e68
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_VLAN_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c72ace7609c2470cab589219d2fd10dcc943e606
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385731"
---
# <a name="oidgenvlanid"></a>OID\_GEN\_VLAN\_ID


为查询，OID\_GEN\_VLAN\_ID OID 报告配置的 VLAN 标识符 (ID) 的 nic。

作为一组 OID\_GEN\_VLAN\_ID OID 指定微型端口驱动程序处理的 NIC 配置的 VLAN 标识符 (ID)。

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

在此请求中传递的信息缓冲区包含 NDIS\_VLAN\_ID 数据类型。 此 NDIS\_VLAN\_ID 值包含在按照 IEEE 802.1Q 12 的最低有效位的 VLAN ID-2005 标准。 更高版本进行排序的 NDIS 位\_VLAN\_ID 值是保留和必须设置为 0。 请注意 NDIS 定义 NDIS\_VLAN\_ULONG 作为 ID。

当传输使用 OID\_GEN\_VLAN\_在查询中，微型端口驱动程序的 ID 返回当前配置的 VLAN ID 的 nic。 一组中使用时，微型端口驱动程序将设置为指定值的 NIC 的当前配置的 VLAN ID。

微型端口驱动程序的过程[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数特定的 NIC，驱动程序的最初设置为零的 NIC 的 VLAN ID。 在驱动程序*MiniportInitializeEx*函数然后读取以下配置参数从注册表中，并，如果存在，参数，则 NIC 的 VLAN ID 设置为参数的值。

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
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)

 

 




