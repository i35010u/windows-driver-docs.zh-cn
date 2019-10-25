---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX 是类似但不同于 OID_WWAN_DEVICE_CAPS 的 OID。
ms.assetid: BE664B41-3FE7-4E93-8739-12BD2F0AE5B8
keywords:
- OID_WWAN_DEVICE_CAPS_EX，每个执行器的 OID，设备功能，例如
ms.date: 04/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 849bed7c32575b91cdd9f428fd129116c2925915
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843864"
---
# <a name="oid_wwan_device_caps_ex"></a>OID\_WWAN\_设备\_CAP\_EX


OID\_WWAN\_设备\_CAP\_EX 类似于[OID\_WWAN\_设备\_cap](oid-wwan-device-caps.md) ，但是每个执行器 oid，不同于 OID_WWAN_DEVICE_CAPS，它是一个每设备 oid。 此 OID 用于指示硬件的设备/执行器功能，包括对扩展可选功能（如 LTE 附加 APN 配置）的功能。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，然后再发送[**ndis\_状态\_WWAN\_设备\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)状态通知，其中包含[**NDIS\_WWAN\_设备\_CAP\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)结构，后者又包含[**WWAN\_设备\_cap\_ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)结构，用于提供有关设备功能的信息。

下图演示了一个查询请求。

![执行器功能查询](images/multi-SIM_6_executorCapabilityQuery.png)

设置请求不适用。

<a name="remarks"></a>备注
-------

驱动程序可以将服务扩展功能作为整体（包括从驱动程序到实际设备）进行报告，这一点很重要。 如果驱动程序支持服务，但基础硬件不支持，则应将服务功能标记为 "FALSE"。

OID\_WWAN\_设备\_CAP\_EX 还用于检索每个执行器的功能。 此 OID 在结构上与[\_WWAN\_设备\_cap](oid-wwan-device-caps.md)的现有 oid 相同，但添加了**执行器 ID**。 微型端口驱动程序应报告它支持的最高 OID 版本。

与[oid\_WWAN\_设备\_cap](oid-wwan-device-caps.md)一样，此 OID 中的参数不应因 SIM 卡而发生更改，而是表示所选执行器的调制解调器 RF 功能。 物理硬件调制解调器可能有多个执行器，因此可能有多个接口支持 OID\_WWAN\_设备\_CAP\_例如。

对于将来可能的更新，如果操作系统的请求版本比设备支持的版本新，则设备应返回它支持的最新版本的 OID 结构。 如果操作系统的请求版本早于设备支持的最新版本，则设备应返回与 OS 规范匹配的版本。 这是一种要求 Ihv 确保所有版本的 OID\_WWAN\_设备\_CAP\_，以支持向后兼容性和旧支持。

不同于 Windows 10 版本1703的其他 Oid，仅在调制解调器支持多 SIM/多执行程序的情况下才需要此 OID，必须为想要在 Windows 10 版本中启动的任何 Microsoft 定义的服务扩展的调制解调器实现1703。

Windows 10 版本1703之前的 Windows 版本仍可使用现有的[OID\_WWAN\_设备\_cap](oid-wwan-device-caps.md);支持多执行器支持的调制解调器的行为不受支持。 Ihv 必须定义此行为。

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10 版本1903开始，OID_WWAN_DEVICE_CAPS_EX 已升级到修订版本2。 如果微型端口驱动程序支持5G，微型端口驱动程序必须使用此 OID 的修订版本2和其中包含的数据结构。

当主机使用此 OID 查询功能时，微型端口驱动程序必须检查底层硬件是否支持5G 手机功能。 如果是这样，微型端口驱动程序会根据硬件功能在[**WWAN_DEVICE_CAPS_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)结构的**WwanDataClass**字段中设置位掩码。

此外，在**WWAN_DEVICE_CAPS_EX**结构的**WwanOptionalServiceCaps**字段中，定义了一个新的可选服务位，它包含对所有新的5G 相关扩展的支持。

有关5G 数据类支持的详细信息，请参阅[MB 5G 数据类支持](mb-5g-data-class-support.md)。

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
<td><p>Windows 10 版本1703</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_设备\_CAP](oid-wwan-device-caps.md)

[ **\_WWAN\_设备\_CAP 的 NDIS\_状态\_EX**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-caps-ex)

[**NDIS\_WWAN\_设备\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

[**WWAN\_设备\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)



