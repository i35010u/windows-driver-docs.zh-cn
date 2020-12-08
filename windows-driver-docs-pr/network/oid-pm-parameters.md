---
title: OID_PM_PARAMETERS
description: 作为查询，协议驱动程序可以使用 OID_PM_PARAMETERS OID 来查询当前启用的网络适配器的电源管理硬件功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 82790eb872aae3a72a70fdd5b9929e344fedc48c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808597"
---
# <a name="oid_pm_parameters"></a>OID \_ PM \_ 参数


作为查询，协议驱动程序可以使用 OID \_ PM \_ 参数 OID 来查询当前启用的网络适配器的电源管理硬件功能。 成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的指针。

作为一个集，协议驱动程序可以使用 OID \_ PM \_ 参数 OID 来启用或禁用网络适配器的当前硬件功能。 协议驱动程序在 [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员中提供了一个指向 [**ndis \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的指针。

<a name="remarks"></a>备注
-------

从 NDIS 6.20 开始，过量协议和筛选器驱动程序使用 OID \_ PM \_ 参数查询和设置当前启用的网络适配器的电源管理硬件功能。

当过量驱动程序查询 OID \_ PM \_ 参数 OID 时，NDIS 完成请求，而不将其转发给微型端口驱动程序。 NDIS 存储请求的设置，并将它们与其他此类请求中的设置组合在一起。 在 NDIS 将网络适配器转换为低功率状态之前，NDIS 会将 set 请求发送到包含 NDIS 存储的所有请求中的组合设置的微型端口驱动程序。

当前启用的功能可以是硬件支持的功能的子集。 有关硬件支持的功能的详细信息，请参阅 [OID \_ PM \_ 硬件 \_ 功能](oid-pm-hardware-capabilities.md)。

**注意** 如果 NDIS \_ \_ \_ \_ 在 [**Ndis \_ pm \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)结构的 **WakeUpFlags** 成员中设置 ndis pm 选择性挂起已启用标志，则它会 \_ \_ 直接向微型端口驱动程序发出 oid pm 参数的 oid 设置请求。 这允许 NDIS 通过网络驱动程序堆栈中的筛选器驱动程序绕过处理。

 

NDIS 或微型端口驱动程序为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS \_ 状态 \_ 缓冲区 \_ 太 \_ 短  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 NDIS OID 请求结构中的成员 BytesNeeded \_ \_ 为所需的最小缓冲区大小。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS \_ 状态 \_ 无效 \_ 参数  
请求失败，因为它尝试启用基础网络适配器不支持的功能。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
由于上述原因之外的原因，导致请求失败。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ PM \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_parameters)

[OID \_ PM \_ 硬件 \_ 功能](oid-pm-hardware-capabilities.md)

 

