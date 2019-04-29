---
title: OID_PM_HARDWARE_CAPABILITIES
description: 为查询，过量驱动程序可以使用 OID_PM_HARDWARE_CAPABILITIES OID 来查询网络适配器的电源管理硬件功能。
ms.assetid: 52446584-bb73-4cf4-bda9-bf92ef2488e3
ms.date: 08/08/2017
keywords: -OID_PM_HARDWARE_CAPABILITIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 46da6ba6459bb342712f07af1d5638cc307bfed0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377579"
---
# <a name="oidpmhardwarecapabilities"></a>OID\_PM\_硬件\_功能


为查询，过量驱动程序可以使用 OID\_PM\_硬件\_功能 OID，若要查询的网络适配器的电源管理硬件功能。 从 OID 查询请求，成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构包含一个指向[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构。

<a name="remarks"></a>备注
-------

NDIS 处理查询的微型端口驱动程序。 从开始 NDIS 6.20，微型端口驱动程序在初始化期间提供的电源管理硬件功能**PowerManagementCapabilitiesEx**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)结构。

微型端口驱动程序必须发出[ **NDIS\_状态\_PM\_功能\_更改**](https://msdn.microsoft.com/library/windows/hardware/ff567410)电源中的报告更改的状态指示管理硬件功能的 NDIS 和基础驱动程序的网络适配器。

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
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。 未请求的微型端口驱动程序。 （请参见备注部分。）</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_微型端口\_适配器\_常规\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565923)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

[**NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)

[**NDIS\_状态\_PM\_功能\_更改**](https://msdn.microsoft.com/library/windows/hardware/ff567410)

 

 




