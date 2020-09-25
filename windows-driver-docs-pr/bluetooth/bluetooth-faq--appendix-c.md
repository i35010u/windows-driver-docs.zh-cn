---
title: 蓝牙附录
description: 包含 Microsoft 定义的蓝牙 HCI 扩展插件示例和关系图。
ms.assetid: 5C3C2479-03F9-4D33-94DA-3371D84C514B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0476e4dc254e524f853923e0ab77bdf0c81f3e19
ms.sourcegitcommit: 68d0aec4c282c9c1e1ab54509c8f4575dd273d56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2020
ms.locfileid: "91221943"
---
# <a name="bluetooth-appendix"></a>蓝牙附录

本部分包含 Microsoft 定义的蓝牙 HCI 扩展插件示例和关系图。

## <a name="example-matching-patterns-for-hci_vs_msft_le_monitor_advertisement"></a>示例：匹配模式 HCI_VS_MSFT_LE_Monitor_Advertisement

此示例显示收到的 HCI_VS_MSFT_LE_Monitor_Advertisement 命令，以及针对命令参数的3个不同播发数据包的评估。

收到 HCI_VS_MSFT_LE_Monitor_Advertisement 命令，控制器接收到 HCI_VS_MSFT_LE_Monitor_Advertisement 命令，其中包含以下参数。

<table>
<tr>
<th>参数</th>
<th>值</th>
<th></th>
</tr>
<tr>
<td>
<p><i>Subcommand_opcode</i></p>
</td>
<td>
<p>0x03</p>
</td>
<td>
<p>HCI_VS_MSFT_LE_Monitor_Advertisement 的子命令操作码</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_high</i></p>
</td>
<td>
<p>0x01</p>
</td>
<td>
<p>1dB</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_low</i></p>
</td>
<td>
<p>0xCE</p>
</td>
<td>
<p>-50dB</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_threshold_low_time_interval</i></p>
</td>
<td>
<p>0x05</p>
</td>
<td>
<p>5 秒</p>
</td>
</tr>
<tr>
<td>
<p><i>RSSI_sampling_period</i></p>
</td>
<td>
<p>0xFF</p>
</td>
<td>
<p>无采样</p>
</td>
</tr>
<tr>
<td>
<p><i>Condition_type</i></p>
</td>
<td>
<p>0x01</p>
</td>
<td>
<p><i>Condition</i> 是一种模式</p>
</td>
</tr>
<tr>
<td rowspan="12">
<p>Condition</p>
</td>
<td>
<p>0x02</p>
</td>
<td>
<p>2个模式应匹配</p>
</td>
</tr>
<tr>
<td>
<p>0x03</p>
</td>
<td>
<p>第一种模式的长度，包括 AD 类型和起始位置</p>
</td>
</tr>
<tr>
<td>
<p>0x01</p>
</td>
<td>
<p>AD 类型</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>AD 类型后面的起始位置</p>
</td>
</tr>
<tr>
<td>
<p>0x01</p>
</td>
<td>
<p>要匹配的第一个模式</p>
</td>
</tr>
<tr>
<td>
<p>0x06</p>
</td>
<td>
<p>第二个模式的长度，包括 AD 类型和起始位置</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
<td>
<p>AD 类型 (制造商特定的数据) </p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>AD 类型后面的起始位置</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td rowspan="4">
<p>要匹配的第二个模式</p>
</td>
</tr>
<tr>
<td>
<p>0x06</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
</tr>
</table>
<p> </p>
然后，控制器接收以下播发数据包。


-    播发数据包 [A] 0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

-    播发数据包 [B] 0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0x01

-    播发数据包 [C] 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

</dd>
</dl>

### <a name="evaluating-match-for-advertisement-packet-a"></a>评估播发数据包的匹配 [A]

<table>
<tr>
<td>
<p>要匹配的第一个模式的 AD 类型</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第一个模式的长度</p>
</td>
<td>
<p>0x03 = 0x01 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型0x01 的位置0x00 处匹配的模式</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型0x01 的位置0x00 处的字节</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第二个模式的 AD 类型</p>
</td>
<td>
<p>0xFF (制造商特定的数据) </p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第二个模式的长度</p>
</td>
<td>
<p>0x06 = 0x04 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型0xFF 的位置0x00 处匹配的模式</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型0xFF 的位置0x00 处的字节</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>判定：通过</b></p>
</td>
</tr>
</table>
  


### <a name="evaluating-match-for-advertisement-packet-b"></a>评估播发数据包的匹配 [B]
<table>
<tr>
<td>
<p>要匹配的第一个模式的 AD 类型</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第一个模式的长度</p>
</td>
<td>
<p>0x03 = 0x01 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型0x01 的位置0x00 处匹配的模式</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型0x01 的位置0x00 处的字节</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第二个模式的 AD 类型</p>
</td>
<td>
<p>0xFF (制造商特定的数据) </p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第二个模式的长度</p>
</td>
<td>
<p>0x06 = 0x04 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型0xFF 的位置0x00 处匹配的模式</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0xff</b></p>
</td>
</tr>
<tr>
<td>
<p>AD 类型0xFF 的位置0x00 处的字节</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0x01</b></p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>判定：通过</b></p>
</td>
</tr>
</table>
 
### <a name="evaluating-match-for-advertisement-packet-c"></a>评估播发数据包的匹配项 [C]
<table>
<tr>
<td>
<p>要匹配的第一个模式的 AD 类型</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第一个模式的长度</p>
</td>
<td>
<p>0x03 = 0x01 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型0x01 的位置0x00 处匹配的模式</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型0x01 的位置0x00 处的字节</p>
</td>
<td>
<p>未定义。 播发没有 AD 类型为0x01 的数据。</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>判定：失败</b></p>
</td>
</tr>
</table>

## <a name="example-advertisement-monitoring"></a>示例：播发监视

此示例演示 RSSI 播发监视。 与指定条件匹配的已接收播发的 RSSI 值如下所示。

<table>
<tr>
<th>时间（秒）</th>
<th>RSSI (dB) </th>
</tr>
<tr>
<td>1</td>
<td>-100</td>
</tr>
<tr>
<td>2</td>
<td>-90</td>
</tr>
<tr>
<td>3</td>
<td>-5</td>
</tr>
<tr>
<td>4</td>
<td>checks.-15-minutes</td>
</tr>
<tr>
<td>5</td>
<td>-30</td>
</tr>
<tr>
<td>6</td>
<td>checks.-15-minutes</td>
</tr>
<tr>
<td>7</td>
<td>-45</td>
</tr>
<tr>
<td>8</td>
<td>-20</td>
</tr>
<tr>
<td>9</td>
<td>-35</td>
</tr>
<tr>
<td>10</td>
<td>-45</td>
</tr>
<tr>
<td>11</td>
<td>-70</td>
</tr>
<tr>
<td>12</td>
<td>-85</td>
</tr>
<tr>
<td>13</td>
<td>-85</td>
</tr>
<tr>
<td>14</td>
<td>-85</td>
</tr>
<tr>
<td>15</td>
<td>-90</td>
</tr>
<tr>
<td>16</td>
<td>-90</td>
</tr>
<tr>
<td>17</td>
<td>-70</td>
</tr>
</table>
<p> </p>
<table>


<table>
<tr>
<th>参数</th>
<th>值</th>
</tr>
<tr>
<td><i>RSSI_threshold_high</i></td>
<td>-10dB</td>
</tr>
<tr>
<td><i>RSSI_threshold_low</i></td>
<td>-80dB</td>
</tr>
<tr>
<td><i>RSSI_threshold_low_time_interval</i></td>
<td>3 秒</td>
</tr>
<tr>
<td><i>RSSI_sampling_period</i></td>
<td>2 秒</td>
</tr>
</table>

</p><img src="images/HCI_Example_Advertisement_Monitoring.png" alt="Advertisement monitoring graph"/><p>

播发 RSSI 大于 RSSI_threshold_high 的时间3。 采样的定期计时器开始时间为3。 每隔2秒，定期计时器将过期，接收的播发的平均 RSSI 值将传播到堆栈。

如果定期计时器在时间5过期，则在这段 ( 时间内收到的 RSSIs 的平均值将) 传播到堆栈。

如果定期计时器在时间13过期，则在此时间范围内收到的播发 RSSIs 的平均值低于 (-80dB) RSSI_threshold_low。 播发 RSSI (-85 dB) 的平均值应传播到主机。

如果 RSSI_threshold_low_time_interval 在瞬间15过期，则会将播发传播到 RSSI 为85dB 的主机。 在此示例中，不会向主机发送更多播发。

 ## <a name="flowchart-advertisement-and-allow-list-filtering"></a>流程图：播发和允许列表筛选

此流程图提供广告筛选的示例控制器实现，并允许在收到广告时进行列表筛选。

当主机收到播发通知或 <MSHelp： link tabindex = "0" 关键字 = "hci_vs_msft_le_monitor_device_event bltooth" 时，控制器可以通过不同方式实现这种逻辑，><b>HCI_VS_MSFT_LE_Monitor_Device_Event</b></mshelp： link> 由流程图指定。

<p><img src="images/HCI_Filtering_Flowchart.png" alt="Microsoft HCI extension filtering flowchart"/></p>

## <a name="sequence-diagram-propagate-scan-response-associated-with-advertisement"></a>序列图：传播与播发关联的扫描响应

序列图：传播与播发关联的扫描响应

当启用活动扫描时，此序列图显示与符合播发筛选器的播发相关联的传播扫描响应。
此关系图只显示控制器和主机之间预期的事件序列，而不显示控制器与特定设备之间的事件。
假设 <i>有一个播发，该播发</i> 满足广告筛选器，而播发 <i>B</i> 不满足播发筛选器。
<p> <img src="images/HCI_Propagate_Scan_Sequence.png" alt="HCI propagate scan sequence diagram"/></p>
