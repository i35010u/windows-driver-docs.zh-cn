---
title: OID_WWAN_SYS_CAPS_INFO
description: OID_WWAN_SYS_CAPS_INFO 检索有关调制解调器的信息。 可以将其发送到调制解调器公开的任何 NDIS 实例上。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SYS_CAPS_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 59d64b6d78ce277e9291a124548ba20961bd7442
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812885"
---
# <a name="oid_wwan_sys_caps_info"></a>OID \_ WWAN \_ SYS \_ CAP \_ 信息


OID \_ WWAN \_ SYS \_ cap \_ 信息检索有关调制解调器的信息。 可以将其发送到调制解调器公开的任何 NDIS 实例上。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，然后再发送 [**ndis \_ 状态 \_ wwan \_ sys \_ \_**](./ndis-status-wwan-sys-caps.md) cap 信息状态通知，其中包含 [**ndis \_ wwan \_ sys \_ \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info) cap 信息结构，该信息又包含一个 [**wwan \_ sys \_ cap \_**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_sys_caps_info) 信息结构，用于提供有关调制解调器总体系统功能的信息。

下图演示了一个查询请求。

![系统功能查询](images/multi-SIM_5_systemCapabilityQuery.png)

设置请求不适用。

<a name="remarks"></a>备注
-------

主机使用 OID \_ WWAN \_ SYS \_ cap \_ 信息来查询调制解调器中 (执行器) 和槽的设备数目，以及可同时处于活动状态的执行器的数目。 双备用调制解调器的并发性为 1;双主动调制解调器的并发性为2。 此 OID 不特定于执行器，并且可以发送到任何 NDIS 实例。

调制解调器可能会公开多个具有不同数量的执行器和槽的配置。 无论选择哪种配置，此查询都将返回当前配置的调制解调器可支持的设备和槽的最大数量。

支持 OID \_ wwan \_ SYS cap 信息的调制解调器 \_ \_ 还应支持[oid \_ wwan \_ 设备 cap， \_ \_ 例如](oid-wwan-device-caps-ex.md) 如果基础调制解调器支持 OID wwan SYS cap 信息，则支持多执行程序调制解调器的 Windows 版本将不会使用旧 [OID \_ wwan \_ 设备 \_ cap](oid-wwan-device-caps.md) \_ \_ \_ \_ 。 对于旧版本的操作系统 (Windows 10 1703 版之前的任何版本，以使此 OID) ，多执行程序的调制解调器会表示为多个独立的调制解调器，并且现有的 OID \_ WWAN \_ 设备 \_ Cap （从 Windows 8 开始提供）将使用。

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
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ WWAN \_ SYS \_ CAP \_ 信息**](./ndis-status-wwan-sys-caps.md)

[**NDIS \_ WWAN \_ SYS \_ CAP \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

[**WWAN \_ SYS \_ CAP \_ 信息**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_sys_caps_info)

[OID \_ WWAN \_ 设备 \_ CAP \_ EX](oid-wwan-device-caps-ex.md)

[OID \_ WWAN \_ 设备 \_ CAP](oid-wwan-device-caps.md)

 

