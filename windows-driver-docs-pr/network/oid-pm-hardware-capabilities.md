---
title: OID_PM_HARDWARE_CAPABILITIES
description: 作为查询，过量驱动程序可以使用 OID_PM_HARDWARE_CAPABILITIES OID 来查询网络适配器的电源管理硬件功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_PM_HARDWARE_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8ce18204726436c7ef61f923fc23b27fece1f947
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249023"
---
# <a name="oid_pm_hardware_capabilities"></a>OID \_ PM \_ 硬件 \_ 功能


作为查询，过量驱动程序可以使用 OID \_ PM \_ 硬件 \_ 功能 oid 来查询网络适配器的电源管理硬件功能。 成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 处理微型端口驱动程序的查询。 从 NDIS 6.20 开始，微型端口驱动程序在 [**ndis \_ 微型端口 \_ 适配器 \_ \_**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的 **PowerManagementCapabilitiesEx** 成员中提供了电源管理硬件功能。

微型端口驱动程序必须发出 [**ndis \_ 状态 \_ PM \_ 功能 \_ 更改**](./ndis-status-pm-capabilities-change.md) 状态指示，将网络适配器的电源管理硬件功能更改报告给 NDIS 和过量驱动程序。

NDIS 为请求返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。 **InformationBuffer** 指向 [**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-buffer-too-short"></a>NDIS \_ 状态 \_ 缓冲区 \_ 太 \_ 短  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 NDIS OID 请求结构中的成员 BytesNeeded \_ \_ 为所需的最小缓冲区大小。

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
<td><p>Version</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。 未请求微型端口驱动程序。 （请参见“备注”部分。）</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

[**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS \_ 状态 \_ PM \_ 功能 \_ 更改**](./ndis-status-pm-capabilities-change.md)

 

