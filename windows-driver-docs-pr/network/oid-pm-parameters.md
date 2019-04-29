---
title: OID_PM_PARAMETERS
description: 为查询，协议驱动程序可以使用 OID_PM_PARAMETERS OID 来查询的电源管理硬件功能的网络适配器的当前已启用。
ms.assetid: c3431724-1b5f-4634-8b1e-27fed9031f01
ms.date: 08/08/2017
keywords: -OID_PM_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 883738803bbaa39c9facddb0016022ce87902953
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383594"
---
# <a name="oidpmparameters"></a>OID\_PM\_参数


为查询，协议驱动程序可以使用 OID\_PM\_参数 OID，若要查询的电源管理硬件功能的网络适配器的当前已启用。 从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构。

作为一组协议驱动程序可以使用 OID\_PM\_参数 OID，若要启用或禁用网络适配器的当前硬件功能。 协议驱动程序提供一个指针指向[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构**InformationBuffer** 的成员[**NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。

<a name="remarks"></a>备注
-------

从开始 NDIS 6.20，基础协议和筛选器驱动程序使用 OID\_PM\_参数来查询和设置当前已启用的硬件功能的网络适配器的电源管理。

当基础驱动程序查询 OID\_PM\_参数 OID、 NDIS 而无需将其转发到微型端口驱动程序完成请求。 NDIS 存储请求的设置，并将它们组合使用其他此类请求中的设置。 NDIS 转换到低功耗状态的网络适配器之前，NDIS 将 set 请求发送到包含从所有 NDIS 存储请求的组合的设置的微型端口驱动程序。

当前已启用的功能可以是硬件支持的功能子集。 有关硬件支持的功能的详细信息，请参阅[OID\_PM\_硬件\_功能](oid-pm-hardware-capabilities.md)。

**请注意**  如果 NDIS 设置 NDIS\_PM\_选择性\_挂起\_中的已启用标志**WakeUpFlags**隶属[ **NDIS\_PM\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566759)结构，它会发出 OID 集请求的 OID\_PM\_直接向微型端口驱动程序的参数。 这允许 NDIS 以网络驱动程序堆栈中的筛选器驱动程序的跳过处理。

 

NDIS 或微型端口驱动程序返回请求的以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
请求已成功完成。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 NDIS 将传递的最终状态代码和结果到 OID 请求完成处理程序的调用方完成请求之后。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS\_状态\_缓冲区\_过\_短  
信息缓冲区太短。 NDIS 集**数据。查询\_信息。BytesNeeded** NDIS 中的成员\_OID\_结构到最小缓冲区大小的请求是必需的。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
请求失败，因为它尝试启用的基础网络适配器不支持的功能。

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
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/ff566759)

[OID\_PM\_硬件\_功能](oid-pm-hardware-capabilities.md)

 

 




