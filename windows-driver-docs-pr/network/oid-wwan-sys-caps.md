---
title: OID_WWAN_SYS_CAPS_INFO
description: OID_WWAN_SYS_CAPS_INFO 检索有关调制解调器的信息。 它可以发送任何公开的调制解调器的 NDIS 实例上。
ms.assetid: D158432A-A715-4ABB-969C-F8F80D2DB845
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SYS_CAPS_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dafacd0c537322ea57ad67e993dc002cbe9bb822
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372497"
---
# <a name="oidwwansyscapsinfo"></a>OID\_WWAN\_SYS\_CAPS\_INFO


OID\_WWAN\_SYS\_CAPS\_信息检索有关调制解调器的信息。 它可以发送任何公开的调制解调器的 NDIS 实例上。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[ **NDIS\_状态\_WWAN\_SYS\_CAP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)状态通知包含[ **NDIS\_WWAN\_SYS\_CAPS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)结构，其中又包含[ **WWAN\_SYS\_CAPS\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_sys_caps_info)结构，以提供有关整体的调制解调器系统功能的信息。

下图说明了查询请求。

![系统功能查询](images/multi-SIM_5_systemCapabilityQuery.png)

不适用集发出的请求。

<a name="remarks"></a>备注
-------

主机使用 OID\_WWAN\_SYS\_CAPS\_信息来查询多个设备 （执行器） 和调制解调器中的槽以及可能会同时处于活动状态的执行器数。 双待机调制解调器者必须并发度为 1;双活动调制解调器者必须并发度为 2。 此 OID 不特定于执行器的可能会发送到任何 NDIS 实例。

调制解调器可能会公开多个具有不同数量的执行器和槽的配置。 无论选择哪种配置，则此查询将返回设备和调制解调器可以支持按当前配置的槽的最大数目。

调制解调器支持 OID\_WWAN\_SYS\_CAP\_信息应该还支持[OID\_WWAN\_设备\_CAPS\_EX](oid-wwan-device-caps-ex.md). 支持多执行器调制解调器的 Windows 版本将不会使用旧[OID\_WWAN\_设备\_CAPS](oid-wwan-device-caps.md)如果基础调制解调器支持 OID\_WWAN\_SYS\_CAPS\_信息。 对于旧版本的操作系统 （任何版本 Windows 10 版本 1703年之前为了进行此 OID），多执行器调制解调器将表示为多个独立的调制解调器和现有的 OID\_WWAN\_设备\_上限可从 Windows 8 开始，将使用。

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


[**NDIS\_STATUS\_WWAN\_SYS\_CAPS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAPS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

[**WWAN\_SYS\_CAPS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_sys_caps_info)

[OID\_WWAN\_DEVICE\_CAPS\_EX](oid-wwan-device-caps-ex.md)

[OID\_WWAN\_DEVICE\_CAPS](oid-wwan-device-caps.md)

 

 




