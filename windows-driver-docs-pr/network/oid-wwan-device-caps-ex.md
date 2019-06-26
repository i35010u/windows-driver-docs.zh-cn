---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX 是从 OID_WWAN_DEVICE_CAPS 一个相似但不同的 OID。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_DEVICE_CAPS_EX，每个执行器，例如设备功能的 OID
ms.date: 04/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6c80b2e2426d94638857e3465d09667fe3c3f7ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362853"
---
# <a name="oidwwandevicecapsex"></a>OID\_WWAN\_DEVICE\_CAPS\_EX


OID\_WWAN\_设备\_CAP\_EX 是类似于[OID\_WWAN\_设备\_CAPS](oid-wwan-device-caps.md)但是每个执行程序 OID，与 OID_WWAN_ 不同这是每个设备 OID DEVICE_CAPS。 此 OID 用于表示硬件的设备/执行程序功能，如 LTE 连接 APN 配置包括扩展的可选功能的功能。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[ **NDIS\_状态\_WWAN\_设备\_CAP\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)状态通知包含[ **NDIS\_WWAN\_设备\_CAPS\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)结构，其中又包含[ **WWAN\_设备\_CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps_ex)结构，以提供有关设备的功能的信息。

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

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10，版本 1903，开始 OID_WWAN_DEVICE_CAPS_EX 已升级到版本 2。 微型端口驱动程序必须使用版本 2 的此 OID 和它包含如果微型端口驱动程序支持 5 个 G 的数据结构。

当使用此 OID 的主机查询功能，微型端口驱动程序必须检查是否基础硬件支持 5g 移动电话功能。 如果是这样，微型端口驱动程序设置的位掩码**WwanDataClass**字段[ **WWAN_DEVICE_CAPS_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps_ex)根据硬件功能的结构。

此外，在**WwanOptionalServiceCaps**字段**WWAN_DEVICE_CAPS_EX**结构，新的可选服务位定义涵盖所有新 5g 相关扩展的支持。

5 G 数据类支持的详细信息，请参阅[MB 5g 数据类支持](mb-5g-data-class-support.md)。

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

[**NDIS\_STATUS\_WWAN\_DEVICE\_CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)

[**NDIS\_WWAN\_DEVICE\_CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

[**WWAN\_DEVICE\_CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps_ex)



