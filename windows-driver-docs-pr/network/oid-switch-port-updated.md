---
title: OID_SWITCH_PORT_UPDATED
description: HYPER-V 可扩展交换机的协议边缘发出一个对象标识符 (OID) 组请求的 OID_SWITCH_PORT_UPDATED 以通知有关可扩展交换机端口的更新的可扩展的交换机扩展。
ms.assetid: 7FDC963A-92E4-49B2-AB77-FA9C92EEBC25
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_PORT_UPDATED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 494258f1a70996145c7023da4b444ca99692dff4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526518"
---
# <a name="oidswitchportupdated"></a>OID\_交换机\_端口\_已更新


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_端口\_经过更新以通知有关可扩展交换机端口的更新的可扩展的交换机扩展。 仅将对端口，已创建，而尚未开始清除/删除进程发出 OID。 目前，仅**PortFriendlyName**创建后受到更新字段。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_保存\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598216)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_切换\_端口\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598229)结构指定的可扩展交换机端口为其更新通知进行了。

扩展必须遵守以下原则处理 OID 设置请求的 OID\_交换机\_端口\_更新：

-   该扩展不能修改[ **NDIS\_交换机\_端口\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598229)与 OID 请求关联的结构。

-   扩展始终将转发对基础扩展的 OID 集请求。 扩展必须不会使请求失败。

**请注意**  可扩展交换机扩展必须发出 OID 集请求的 OID\_切换\_端口\_已更新。

 

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 集请求的 OID\_切换\_端口\_已更新，并返回以下状态代码。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>状态代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>NDIS_STATUS_SUCCESS</p></td>
<td><p>OID 请求已成功完成。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


****
[*DereferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598141)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_交换机\_端口\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598229)

[**NdisFOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561830)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://msdn.microsoft.com/library/windows/hardware/hh598294)

 

 




