---
title: NDIS_STATUS_PM_HARDWARE_CAPABILITIES
description: NDIS_STATUS_PM_HARDWARE_CAPABILITIES 状态向过量驱动程序表明网络适配器的电源管理（PM）硬件功能发生变化。
ms.assetid: A4AACA48-DCD2-44FA-B016-52C37EE9A1D6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_HARDWARE_CAPABILITIES 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ef77df27720c7ec00afb1a1d750712feddbf966b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843540"
---
# <a name="ndis_status_pm_hardware_capabilities"></a>NDIS\_状态\_PM\_硬件\_功能


**NDIS\_状态\_PM\_硬件\_功能**状态指示过量驱动程序网络适配器的电源管理（PM）硬件功能发生变化。

<a name="remarks"></a>备注
-------

当需要对以前报告的电源管理功能进行更新时，微型端口驱动程序将生成**NDIS\_状态\_PM\_硬件\_功能**状态指示。

802.11 网络适配器的微型端口驱动程序可以生成此状态指示。

提供负载平衡故障转移（LBFO）支持的 MUX 中间驱动程序还可以生成此状态指示。 MUX 驱动程序聚合属于 LBFO 团队的基础网络适配器的 PM 功能。 如果 PM 功能发生更改，原因是已在团队中添加或删除适配器，则 MUX 驱动程序必须生成此状态指示。 有关 LBFO MUX 中间驱动程序的详细信息，请参阅[NDIS Mux 中间驱动程序](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-mux-intermediate-drivers)。

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含一个指向[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的指针，该指针具有更新的电源管理功能。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

 




