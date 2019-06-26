---
title: OID_SWITCH_NIC_UPDATED
description: HYPER-V 可扩展交换机的协议边缘可扩展交换机驱动程序堆栈向发出 OID_SWITCH_NIC_UPDATED 的对象标识符 (OID) 集请求。
ms.assetid: C1B446A3-861F-41B4-99EF-C7CB45F86F39
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_SWITCH_NIC_UPDATED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 961da96e3927cc093e9f5b945c466dd18bb5f087
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366573"
---
# <a name="oidswitchnicupdated"></a>OID\_交换机\_NIC\_已更新


HYPER-V 可扩展交换机的协议边缘发出对象标识符 (OID) 组请求的 OID\_切换\_NIC\_更新为可扩展交换机驱动程序堆栈。 此 OID 请求通知基础可扩展交换机扩展有关的网络适配器的参数的更新。 只能将 Nic 已连接，但尚未开始断开连接进程发出 OID。 这些运行时配置更改可以包括**NicFriendlyName**， **NetCfgInstanceId**， **MTU**， **NumaNodeId**， **PermanentMacAddress**， **VMMacAddress**， **CurrentMacAddress**，和**VFAssigned**。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_交换机\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构。

<a name="remarks"></a>备注
-------

**PortId**的成员[ **NDIS\_开关\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定的端口为其更新正在进行通知。 可扩展交换机扩展可以通过发出的 OID 查询请求获取此信息以及其他端口可扩展交换机上的参数信息[OID\_切换\_端口\_数组](oid-switch-port-array.md)。

**索引**的成员[ **NDIS\_开关\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)结构指定的网络适配器的索引为其更新通知进行了。 使用指定的网络适配器**索引**值连接到指定的可扩展交换机端口**PortId**成员。 有关这些索引值的详细信息，请参阅[网络适配器索引值](https://docs.microsoft.com/windows-hardware/drivers/network/network-adapter-index-values)。

扩展必须遵守以下原则处理 OID 设置请求的 OID\_交换机\_NIC\_更新：

-   该扩展不能修改[ **NDIS\_交换机\_NIC\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)与 OID 请求关联的结构。
-   扩展始终将转发对基础扩展的 OID 集请求。 扩展必须完成请求。
-   扩展必须发出其自己的 OID 的 OID 集请求\_交换机\_NIC\_已更新。

### <a name="return-status-codes"></a>返回状态代码

可扩展交换机的基础的微型端口边缘完成 OID 查询请求的 OID\_切换\_NIC\_已更新，并返回以下状态代码。

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
[*DereferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_dereference_switch_nic)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_SWITCH\_NIC\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_switch_nic_parameters)

[OID\_交换机\_NIC\_断开连接](oid-switch-nic-disconnect.md)

[OID\_交换机\_端口\_数组](oid-switch-port-array.md)

[*ReferenceSwitchNic*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_reference_switch_nic)

 

 




