---
title: OID_WWAN_SYS_CAPS_INFO
description: OID_WWAN_SYS_CAPS_INFO 检索有关调制解调器的信息。 可以将其发送到调制解调器公开的任何 NDIS 实例上。
ms.assetid: D158432A-A715-4ABB-969C-F8F80D2DB845
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SYS_CAPS_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1e7a427d5cb7372ef5d7675917dc31c6979013bb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843778"
---
# <a name="oid_wwan_sys_caps_info"></a>OID\_WWAN\_SYS\_CAP\_信息


OID\_WWAN\_SYS\_CAP\_信息检索有关调制解调器的信息。 可以将其发送到调制解调器公开的任何 NDIS 实例上。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，然后再发送[**ndis\_状态\_WWAN\_SYS\_CAP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)状态通知，其中包含一个[**NDIS\_WWAN\_SYS\_CAP\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)结构，后者又包含一个[**WWAN\_SYS\_cap\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_sys_caps_info)结构，用于提供有关调制解调器整体系统功能的信息。

下图演示了一个查询请求。

![系统功能查询](images/multi-SIM_5_systemCapabilityQuery.png)

设置请求不适用。

<a name="remarks"></a>备注
-------

主机使用 OID\_WWAN\_SYS\_CAP\_信息来查询调制解调器中的设备（执行器）和槽的数目，以及可同时处于活动状态的执行器的数目。 双备用调制解调器的并发性为 1;双主动调制解调器的并发性为2。 此 OID 不特定于执行器，并且可以发送到任何 NDIS 实例。

调制解调器可能会公开多个具有不同数量的执行器和槽的配置。 无论选择哪种配置，此查询都将返回当前配置的调制解调器可支持的设备和槽的最大数量。

支持 OID\_WWAN\_SYS\_CAP\_信息的调制解调器应还支持[oid\_wwan\_](oid-wwan-device-caps-ex.md)\_\_ 支持多执行程序调制解调器的 Windows 版本将不会使用旧[OID\_wwan\_设备\_cap](oid-wwan-device-caps.md) ，前提是基础调制解调器支持 OID\_WWAN\_SYS\_CAP\_信息。 对于旧版本的操作系统（在 Windows 10 版本1703之前的任何版本，出于此 OID 目的），多执行程序的调制解调器会表示为多个独立的调制解调器，\_WWAN\_设备\_CAP 的现有 OID 可用从 Windows 8 开始，将使用。

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


[**NDIS\_状态\_WWAN\_SYS\_CAP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

[**WWAN\_SYS\_CAP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_sys_caps_info)

[OID\_WWAN\_设备\_CAP\_EX](oid-wwan-device-caps-ex.md)

[OID\_WWAN\_设备\_CAP](oid-wwan-device-caps.md)

 

 




