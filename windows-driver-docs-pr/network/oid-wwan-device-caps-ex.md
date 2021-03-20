---
title: OID_WWAN_DEVICE_CAPS_EX
description: OID_WWAN_DEVICE_CAPS_EX 与 OID_WWAN_DEVICE_CAPS 类似但不同。
keywords:
- OID_WWAN_DEVICE_CAPS_EX，每个执行器 OID，设备功能，例如
ms.date: 04/04/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b1d3bc291b94b7f21e5a93b0307fa2f2cd0f9af9
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719494"
---
# <a name="oid_wwan_device_caps_ex"></a>OID \_ WWAN \_ 设备 \_ CAP \_ EX


OID \_ wwan \_ 设备 \_ Cap \_ 类似于 [oid \_ wwan \_ 设备 \_ cap](oid-wwan-device-caps.md) ，但它是每个执行器 oid，这与 OID_WWAN_DEVICE_CAPS 这是一个每设备 oid 的情况不同。 此 OID 用于指示硬件的设备/执行器功能，包括对扩展可选功能（如 LTE 附加 APN 配置）的功能。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ 原始请求所需的 ndis 状态指示，之后再 \_ 发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ cap \_**](./ndis-status-wwan-device-caps-ex.md) （包含 [**Ndis \_ wwan \_ 设备 \_ \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex) cap ex 结构，后者又包含一个 [**wwan \_ 设备 \_ cap \_ ex**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex) 结构）来提供有关设备功能的信息。

下图演示了一个查询请求。

![执行器功能查询](images/multi-SIM_6_executorCapabilityQuery.png)

设置请求不适用。

<a name="remarks"></a>备注
-------

驱动程序可以将服务扩展功能作为整体（包括从驱动程序到实际设备）进行报告，这一点很重要。 如果驱动程序支持服务，但基础硬件不支持，则应将服务功能标记为 "FALSE"。

OID \_ WWAN \_ 设备 \_ cap \_ EX 还用于检索每个执行器的功能。 此 OID 在结构上与现有的 [oid \_ WWAN \_ 设备 \_ cap](oid-wwan-device-caps.md) 相同，但添加了执行器 **ID**。 微型端口驱动程序应报告它支持的最高 OID 版本。

与 [oid \_ WWAN \_ 设备 \_ CAP](oid-wwan-device-caps.md)一样，此 OID 中的参数不应因 SIM 卡而发生更改，而是表示所选执行器的调制解调器 RF 功能。 物理硬件调制解调器可能有多个执行器，因此可能具有多个支持 OID \_ WWAN \_ 设备 cap 的接口， \_ \_ 例如

对于将来可能的更新，如果操作系统的请求版本比设备支持的版本新，则设备应返回它支持的最新版本的 OID 结构。 如果操作系统的请求版本早于设备支持的最新版本，则设备应返回与 OS 规范匹配的版本。 需要使用 Ihv 确保 OID WWAN 设备 cap 的所有修订版本 \_ \_ \_ \_ 都支持向后兼容性和旧支持。

不同于 Windows 10 版本1703的其他 Oid，只是在调制解调器支持多 SIM/多执行程序的情况下才需要此 OID，因此必须为想要支持从 Windows 10 版本1703开始的任何 Microsoft 定义的服务扩展的调制解调器实现此 OID。

Windows 10 版本1703之前的 Windows 版本仍可使用现有的 [OID \_ WWAN \_ 设备 \_ cap](oid-wwan-device-caps.md); 对于多执行器支持的调制解调器，它们的行为不受支持。 Ihv 必须定义此行为。

### <a name="windows-10-version-1903"></a>Windows 10 版本 1903

从 Windows 10 1903 版开始，OID_WWAN_DEVICE_CAPS_EX 已升级到修订版本2。 如果微型端口驱动程序支持5G，微型端口驱动程序必须使用此 OID 的修订版本2和其中包含的数据结构。

当主机使用此 OID 查询功能时，微型端口驱动程序必须检查底层硬件是否支持5G 手机功能。 如果是这样，微型端口驱动程序会根据硬件功能在 [**WWAN_DEVICE_CAPS_EX**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)结构的 **WwanDataClass** 字段中设置位掩码。

此外，在 **WWAN_DEVICE_CAPS_EX** 结构的 " **WwanOptionalServiceCaps** " 字段中，定义了一个新的可选服务位，它包含所有新5G 相关扩展的支持。

有关5G 数据类支持的详细信息，请参阅 [MB 5G 数据类支持](./mb-5g-operations-overview.md)。

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
<td><p>Windows 10 版本 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WWAN \_ 设备 \_ CAP](oid-wwan-device-caps.md)

[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ CAP \_ EX**](./ndis-status-wwan-device-caps-ex.md)

[**NDIS \_ WWAN \_ 设备 \_ CAP \_ EX**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

[**WWAN \_ 设备 \_ CAP \_ EX**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps_ex)