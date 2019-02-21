---
title: OID_PM_CURRENT_CAPABILITIES
description: 为查询，过量驱动程序可以使用 OID_PM_CURRENT_CAPABILITIES OID 来查询网络适配器的当前可用的电源管理功能。
ms.assetid: b35ce325-a1aa-43e0-bf68-cb2ab89dff76
ms.date: 08/08/2017
keywords: -OID_PM_CURRENT_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6f4fd0cffb105e0fd6967d118f8e0c33df59f1ef
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547879"
---
# <a name="oidpmcurrentcapabilities"></a>OID\_PM\_当前\_功能


为查询，过量驱动程序可以使用 OID\_PM\_当前\_功能 OID，若要查询的网络适配器的当前可用的电源管理功能。 从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

<a name="remarks"></a>备注
-------

NDIS 处理查询的微型端口驱动程序。 从 NDIS 6.20 开始，则微型端口驱动程序提供在初始化期间的电源管理硬件功能。 但是，NDIS 可以隐藏来自协议驱动程序的一些功能。 例如，NDIS 可能会报告不同的功能，当用户禁用部分或全部的电源管理功能。

请注意，NDIS 报告给协议驱动程序的当前电源管理功能不一定是到 NDIS 微型端口驱动程序报告的硬件功能相同。

NDIS 报告到过量协议中的驱动程序的电源管理功能的基础的网络适配器**PowerManagementCapabilitiesEx**的成员[ **NDIS\_绑定\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff564832)绑定操作过程中的结构。 因此，协议驱动程序不需要查询 OID。

NDIS 问题[ **NDIS\_状态\_PM\_功能\_更改**](https://msdn.microsoft.com/library/windows/hardware/ff567410)状态指示报表中的更改电源管理可供过量驱动程序的功能。

NDIS 基础的网络适配器有 NDIS 6.1 或较旧的微型端口驱动程序，如果转换到的基础网络适配器的电源管理功能[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

NDIS 返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。 **InformationBuffer**指向[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求之后。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求失败，而原因并非前面的原因。

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
<td><p>标头</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_BIND\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff564832)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状态\_PM\_功能\_更改**](https://msdn.microsoft.com/library/windows/hardware/ff567410)

 

 




