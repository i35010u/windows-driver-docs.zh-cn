---
title: WDI_TLV_START_AP_PARAMETERS
description: WDI_TLV_START_AP_PARAMETERS 是包含的参数为 OID_WDI_TASK_START_AP TLV。
ms.assetid: 6791754C-9786-4BE4-9915-7333E4E0AFB8
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_START_AP_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b71a39ca9811b03a234e3afe89598b18bf9e1eae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330431"
---
# <a name="wditlvstartapparameters"></a>WDI\_TLV\_START\_AP\_PARAMETERS


WDI\_TLV\_启动\_AP\_参数是包含参数的 TLV [OID\_WDI\_任务\_启动\_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964).

## <a name="tlv-type"></a>TLV 类型


0xAB

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT32</td>
<td>信号周期中。 如果非零，则此参数指定的信号时间间隔。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>DTIM 段。 如果非零，则此参数指定传输的信息帧，其中包含一个等于零的 DTIM 计数字段与 TIM 元素之间的信号间隔数。 此值被传输信息帧的 DTIM 段字段中。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>此参数设置 dot11ExcludeUnencrypted MIB。 有效值为 0 和 1。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>此参数指定设备是否支持 802.11b 速度。 有效值为 0 （不支持） 和 1 （支持）。 当此值设置为 1 时，访问点应允许客户端使用 11b 费率若要连接到它。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>在 Windows 10 版本 1511，WDI 版本 1.0.10 中添加。
<p>此参数指定是否允许旧 SoftAP 客户端连接。 有效值为 0 （不允许） 和 1 （允许）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>在 Windows 10 版本 1511，WDI 版本 1.0.10 中添加。
<p>MustUseSpecifiedChannels。 此参数指定是否在 AP，仅可以在中指定的通道上启动<a href="https://msdn.microsoft.com/library/windows/hardware/dn925964" data-raw-source="[OID_WDI_TASK_START_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)">OID_WDI_TASK_START_AP</a>任务的参数<a href="wdi-tlv-ap-band-channel.md" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](wdi-tlv-ap-band-channel.md)"> <strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>。 有效值为 0 和 1。 如果设置为 1，AP 只能启动从指定的列表。 如果未设置，该列表旨在提供建议的固件，可以选择的通道和它可能会选取另一个通道，如果不能在任何指定的通道上启动 AP。</p></td>
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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WDI\_TASK\_START\_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)

 

 




