---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX 是从 OID_WWAN_DEVICE_CAPS 一个相似但不同的 OID。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_DEVICE_CAPS_EX，每个执行器，例如设备功能的 OID
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89347328408ea03295a7c1ddc2b9d35bb4d56abe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566391"
---
# <a name="oidwwandevicecapsex"></a>OID\_WWAN\_DEVICE\_CAPS\_EX


OID\_WWAN\_设备\_CAP\_EX 是从一个相似但不同的 OID [OID\_WWAN\_设备\_CAPS](oid-wwan-device-caps.md)。 OID\_WWAN\_设备\_CAPS\_EX 是每个执行程序 OID。 此 OID 用于表示硬件的设备/执行程序功能，如 LTE 连接 APN 配置包括扩展的可选功能的功能。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[ **NDIS\_状态\_WWAN\_设备\_CAP\_EX** ](https://msdn.microsoft.com/library/windows/hardware/mt782396)状态通知包含[ **NDIS\_WWAN\_设备\_CAPS\_EX** ](https://msdn.microsoft.com/library/windows/hardware/mt782401)结构，其中又包含[ **WWAN\_设备\_CAPS\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt799889)结构，以提供有关设备的功能的信息。

下图说明了查询请求。

![执行器功能查询](images/multi-SIM_6_executorCapabilityQuery.png)

不适用集发出的请求。

<a name="remarks"></a>备注
-------

它是作为一个整体到实际设备驱动程序中包括的报表服务扩展功能的驱动程序的关键。 如果驱动程序支持一种服务，但不是受基础硬件，则服务功能应标记为 FALSE。

OID\_WWAN\_设备\_CAPS\_EX 也用于检索每个执行器的功能。 此 OID 是作为现有结构中相同[OID\_WWAN\_设备\_CAPS](oid-wwan-device-caps.md)但添加了**执行器 ID**。 微型端口驱动程序应报告它支持的最高 OID 版本。

正如使用[OID\_WWAN\_设备\_CAPS](oid-wwan-device-caps.md)，此 OID 中的参数不应因 SIM 卡而更改，但而是表示所选的执行器的调制解调器的 RF 功能。 物理硬件调制解调器可能有多个执行器，因而可能使多个接口，它们支持 OID\_WWAN\_设备\_CAPS\_资源.

对于可能未来的更新，如果操作系统的请求的版本高于设备支持的版本，设备应返回它支持的 OID 结构的最新版本。 如果操作系统的请求的版本早于设备支持的最新项目，则设备应返回匹配的操作系统的规范的版本。 它是必需的 Ihv 以确保所有修订的 OID\_WWAN\_设备\_CAPS\_EX 是支持向后兼容性和旧的支持。

与不同的是其他 Oid 熟悉 Windows 10 版本 1703年才需要如果调制解调器支持多 SIM/多-执行器数目，此 OID 必须实现为想要支持从 Windows 10 版本的任何 Microsoft 定义的服务扩展的调制解调器1703。

在 Windows 10 版本 1703年之前的 Windows 版本仍可以使用现有[OID\_WWAN\_设备\_CAPS](oid-wwan-device-caps.md); 它们与多执行器能够调制解调器的行为不受支持的方案。 Ihv 必须定义此行为。

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
<td><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_DEVICE\_CAPS](oid-wwan-device-caps.md)

[**NDIS\_STATUS\_WWAN\_DEVICE\_CAPS\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt782396)

[**NDIS\_WWAN\_DEVICE\_CAPS\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt782401)

[**WWAN\_DEVICE\_CAPS\_EX**](https://msdn.microsoft.com/library/windows/hardware/mt799889)



