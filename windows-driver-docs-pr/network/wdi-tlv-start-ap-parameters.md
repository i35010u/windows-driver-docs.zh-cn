---
title: WDI_TLV_START_AP_PARAMETERS
description: WDI_TLV_START_AP_PARAMETERS 为 TLV，其中包含 OID_WDI_TASK_START_AP 的参数。
ms.assetid: 6791754C-9786-4BE4-9915-7333E4E0AFB8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_START_AP_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f96341ef5fbdb1fd75996fe857c5ed726b6829c
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107136"
---
# <a name="wdi_tlv_start_ap_parameters"></a>WDI \_ TLV \_ 启动 \_ AP \_ 参数


WDI \_ tlv \_ 启动 \_ ap \_ 参数是一个 TLV，其中包含 [OID \_ WDI \_ 任务 \_ 启动 \_ AP](./oid-wdi-task-start-ap.md)的参数。

## <a name="tlv-type"></a>TLV 类型


0xAB

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>信标时间段。 如果非零，则此参数指定信号间隔。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>DTIM 时间段。 如果非零，则此参数指定两次传输包含具有等于零的 DTIM Count 字段的 TIM 元素的信标帧之间的信标间隔数。 此值在信标帧的 DTIM Period 字段中传输。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>此参数设置 dot11ExcludeUnencrypted MIB。 有效值为0和1。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>此参数指定设备是否支持 802.11 b 速度。 有效值为 0 (不支持) 和 1 (支持) 。 如果此值设置为1，则访问点应允许使用11b 速率的客户端连接到它。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>已在 Windows 10 版本1511、WDI 版本1.0.10 中添加。
<p>此参数指定是否允许旧的 SoftAP 客户端连接。 有效值为 0 (不允许) ， (允许的值为 1) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>已在 Windows 10 版本1511、WDI 版本1.0.10 中添加。
<p>MustUseSpecifiedChannels. 此参数指定是否只能在<a href="wdi-tlv-ap-band-channel.md" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](wdi-tlv-ap-band-channel.md)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a> <a href="/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](./oid-wdi-task-start-ap.md)">OID_WDI_TASK_START_AP</a>任务参数中指定的通道上启动 AP。 有效值为0和1。 如果设置为1，则只能从指定列表启动 AP。 如果未设置此列表，则该列表应是固件可以选取的通道的建议，如果不能在任何指定的通道上启动 AP，则可以选择另一个通道。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 任务 \_ 启动 \_ AP](./oid-wdi-task-start-ap.md)

