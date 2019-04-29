---
title: OID_SWITCH_NIC_DISCONNECT
description: 协议边缘的 HYPER-V 可扩展交换机对象标识符 (OID) 设置的 OID_SWITCH_NIC_DISCONNECT 的请求，以通知基础正在可扩展交换机端口和网络适配器之间的连接的可扩展的交换机扩展的问题在拆解。 该连接，则完全将调用后，可扩展交换机的协议边缘将发出 OID_SWITCH_NIC_DELETE OID 集请求。
ms.assetid: 367081A7-F259-4132-B857-C956C0F2829C
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_DISCONNECT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b60e836b625a6b24a145ce1900fac299874b428d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355913"
---
# <a name="oidswitchnicdisconnect"></a>OID\_交换机\_NIC\_断开连接


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_断开连接，以通知基础可扩展交换机扩展的之间的连接可扩展的交换机端口和一个网络适配器被被撤销。 可扩展交换机的协议边缘连接完全销毁后，将颁发的 OID 集请求[OID\_切换\_NIC\_删除](oid-switch-nic-delete.md)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构。

<a name="remarks"></a>备注
-------

**索引**的成员[ **NDIS\_开关\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)结构指定的网络适配器的索引为其断开连接通知进行了。 使用指定的网络适配器**索引**值连接到指定的可扩展交换机端口**PortId**成员。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

扩展必须处理的 OID 的 OID 集请求时请遵循以下准则\_交换机\_NIC\_断开连接：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh598215)与 OID 请求关联的结构。

-   OID\_切换\_NIC\_断开连接请求仅通知可扩展交换机连接，则在将调用指定的网络适配器和可扩展的交换机端口之间的扩展。 扩展处理此 OID 请求后，它必须执行以下操作：

    -   生成可扩展的交换机端口上为其网络适配器连接到的任何数据包流量 OID\_切换\_NIC\_发出断开连接的 OID 请求。

    -   调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)可扩展交换机端口上指定的网络适配器连接的可扩展交换机引用计数器递增。

    -   转发或源于的 OID 请求[OID\_交换机\_NIC\_请求](oid-switch-nic-request.md)到为其基础网络适配器 OID\_开关\_NIC\_发出断开连接 OID 请求。

        **请注意**如果该扩展调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增前 OID 的可扩展交换机引用计数器\_切换\_NIC\_断开连接颁发、 扩展仍然可以转发或源自 OID 请求。



    -   转发或源于的 NDIS 状态迹象[ **NDIS\_状态\_交换机\_NIC\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh598205)从为其基础网络适配器OID\_交换机\_NIC\_发出断开连接的 OID 请求。

        **请注意**如果该扩展调用[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增前 OID 的可扩展交换机引用计数器\_切换\_NIC\_断开连接颁发、 扩展仍然可以转发或源自 NDIS 状态指示。

        **请注意**如果该扩展以前称为[ *ReferenceSwitchNic* ](https://msdn.microsoft.com/library/windows/hardware/hh598294)递增可扩展交换机引用计数器，它不需要同步其调用来源或转发OID 请求或管理的 HYPER-V 可扩展其代码与的 NDIS 状态指示切换 OID 请求。 扩展递增引用计数器后，可扩展交换机接口不会颁发的 OID 集请求[OID\_切换\_NIC\_删除](oid-switch-nic-delete.md)。

-   扩展始终将转发对基础扩展的 OID 集请求。 扩展必须完成请求。

-   可扩展交换机外部网络适配器可以绑定到一个或多个基础物理适配器。 对于每个绑定到外部网络适配器的物理网络适配器，可扩展交换机的协议边缘会发出一个单独的 OID 集请求的 OID\_切换\_NIC\_断开连接。 每个 OID 集请求指定一个不同的网络适配器连接的索引值。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://msdn.microsoft.com/library/windows/hardware/hh598258)。

    扩展必须维护每个基础物理适配器的连接状态。 有关在其中的物理网络适配器可以绑定到外部网络适配器的不同配置的详细信息，请参阅[的物理网络适配器配置的类型](https://msdn.microsoft.com/library/windows/hardware/hh582274)。

**请注意**扩展必须发出其自己的 OID 的 OID 集请求\_交换机\_NIC\_断开连接。

有关可扩展交换机端口和网络适配器连接的状态的详细信息，请参阅[HYPER-V 可扩展交换机端口和网络适配器状态](https://msdn.microsoft.com/library/windows/hardware/hh598182)。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_NIC\_断开连接，并返回以下状态代码。

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
<td><p>Version</p></td>
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh598215)

[OID\_交换机\_NIC\_删除](oid-switch-nic-delete.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchPort*](https://msdn.microsoft.com/library/windows/hardware/hh598295)