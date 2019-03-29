---
title: 蓝牙附录
description: 包含 Microsoft 定义蓝牙 HCI 扩展插件的示例和关系图。
ms.assetid: 5C3C2479-03F9-4D33-94DA-3371D84C514B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50c566181f27f386cc1a0912e3044587e46e70f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575221"
---
# <a name="bluetooth-appendix"></a>蓝牙附录

本部分包含 Microsoft 定义蓝牙 HCI 扩展插件的示例和关系图。

## <a name="example-matching-patterns-for-hcivsmsftlemonitoradvertisement"></a>例如：有关 HCI_VS_MSFT_LE_Monitor_Advertisement 匹配模式
此示例演示已接收的 HCI_VS_MSFT_LE_Monitor_Advertisement 命令，并根据命令参数的 3 个不同的通告数据包的评估。

接收到的 HCI_VS_MSFT_LE_Monitor_Advertisement 命令 HCI_VS_MSFT_LE_Monitor_Advertisement 命令控制器收到并包含以下参数。

<table>
<tr>
<th>参数</th>
<th>ReplTest1</th>
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
<p>子操作码命令为 HCI_VS_MSFT_LE_Monitor_Advertisement</p>
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
<p>任何采样</p>
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
<p><i>条件</i>是一种模式</p>
</td>
</tr>
<tr>
<td rowspan="12">
<p><i>Condition</i></p>
</td>
<td>
<p>0x02</p>
</td>
<td>
<p>应匹配 2 模式</p>
</td>
</tr>
<tr>
<td>
<p>0x03</p>
</td>
<td>
<p>第一个模式，包括 AD 类型和开始位置的长度</p>
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
<p>以下类型的 AD 的起始位置</p>
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
<p>第二个模式，包括 AD 类型和开始位置的长度</p>
</td>
</tr>
<tr>
<td>
<p>0xFF</p>
</td>
<td>
<p>AD 类型 （制造商特定的数据）</p>
</td>
</tr>
<tr>
<td>
<p>0x00</p>
</td>
<td>
<p>以下类型的 AD 的起始位置</p>
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
在控制器则将收到以下通告数据包。


-    播发数据包 [A] 0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

-    播发数据包 [B] 0x02 0x01 0x01 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0x01

-    播发数据包 [C] 0x07 0x09 0x54 0x61 0x62 0x6C 0x65 0x74 0x05 0xFF 0x00 0x06 0xFF 0xFF

</dd>
</dl>

### <a name="evaluating-match-for-advertisement-packet-a"></a>评估播发数据包 [A] 的匹配项

<table>
<tr>
<td>
<p>AD 类型的第一种模式进行匹配</p>
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
<p>0x03-0x02 = 0x01 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型 0x01 0x00 位置匹配的模式</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型 0x01 0x00 位置处的字节数</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型的第二个模式进行匹配</p>
</td>
<td>
<p>0xFF （制造商特定的数据）</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第二个模式的长度</p>
</td>
<td>
<p>0x06-0x02 = 0x04:sp 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型 0xFF 0x00 位置匹配的模式</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型 0xFF 0x00 位置处的字节数</p>
</td>
<td>
<p>0x00 0x06 0xFF 0xFF</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>结论：PASS</b></p>
</td>
</tr>
</table>
  


### <a name="evaluating-match-for-advertisement-packet-b"></a>评估播发数据包 [B] 的匹配项
<table>
<tr>
<td>
<p>AD 类型的第一种模式进行匹配</p>
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
<p>0x03-0x02 = 0x01 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型 0x01 0x00 位置匹配的模式</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型 0x01 0x00 位置处的字节数</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型的第二个模式进行匹配</p>
</td>
<td>
<p>0xFF （制造商特定的数据）</p>
</td>
</tr>
<tr>
<td>
<p>要匹配的第二个模式的长度</p>
</td>
<td>
<p>0x06-0x02 = 0x04:sp 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型 0xFF 0x00 位置匹配的模式</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0xFF</b></p>
</td>
</tr>
<tr>
<td>
<p>AD 类型 0xFF 0x00 位置处的字节数</p>
</td>
<td>
<p>0x00 0x06 0xFF <b>0x01</b></p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>结论：PASS</b></p>
</td>
</tr>
</table>
 
### <a name="evaluating-match-for-advertisement-packet-c"></a>评估适合播发数据包 [C]
<table>
<tr>
<td>
<p>AD 类型的第一种模式进行匹配</p>
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
<p>0x03-0x02 = 0x01 字节</p>
</td>
</tr>
<tr>
<td>
<p>要在 AD 类型 0x01 0x00 位置匹配的模式</p>
</td>
<td>
<p>0x01</p>
</td>
</tr>
<tr>
<td>
<p>AD 类型 0x01 0x00 位置处的字节数</p>
</td>
<td>
<p>未定义。 播发不具有与 AD 类型 0x01 的数据。</p>
</td>
</tr>
<tr>
<td colspan="2">
<p><b>结论：FAIL</b></p>
</td>
</tr>
</table>

## <a name="example-advertisement-monitoring"></a>例如：播发监视

此示例说明了 RSSI 播发监视。 匹配指定的条件的已接收播发的 RSSI 值如下所示。

<table>
<tr>
<th>时间（秒）</th>
<th>RSSI (dB)</th>
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
<td>-15</td>
</tr>
<tr>
<td>5</td>
<td>-30</td>
</tr>
<tr>
<td>6</td>
<td>-15</td>
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

播发 RSSI 大于 RSSI_threshold_high 3 次。 在时间 3 启动定期计时器采样。 每隔 2 秒，定期计时器过期并已接收播发的平均 RSSI 值传播到堆栈。

在此期间定期计时器过期时在 5 时，收到的播发 RSSIs 平均值 (-23dB) 传播到堆栈。

定期计时器过期时在时 13，播发 RSSIs 接收在此时间范围内的平均值低于 RSSI_threshold_low (-80dB)。 播发 RSSI (-85 dB) 的平均应传播到主机。

当 RSSI_threshold_low_time_interval 过期即时 15 时，播发将传播到具有的-85dB RSSI 的主机。 没有更多的播发发送到在此示例中的主机。

 ## <a name="flowchart-advertisement-and-white-list-filtering"></a>流程图：播发和白名单筛选

此流程图提供了播发筛选和白名单筛选收到播发时的示例控制器实现。

控制器可以只要在播发通知宿主，以不同方式，实现此逻辑或 < MSHelp:link tabindex ="0"keywords="bltooth.hci_vs_msft_le_monitor_device_event"><b>HCI_VS_MSFT_LE_Monitor_Device_Event</b>< / MSHelp:link > 所指定的流程图。

<p><img src="images/HCI_Filtering_Flowchart.png" alt="Microsoft HCI extension filtering flowchart"/></p>


## <a name="sequence-diagram-propagate-scan-response-associated-with-advertisement"></a>序列图：传播与播发相关联的扫描响应

序列图：传播与播发相关联的扫描响应

此序列图显示了与播发时启用 active 扫描满足播发筛选器相关联的传播扫描响应。
此图仅显示预期的控制器和主机之间的事件顺序并不会显示在控制器和特定的设备之间的事件。
假设为播发<i>A</i>满足播发筛选器和播发<i>B</i>中不满足播发筛选器。
<p> <img src="images/HCI_Propagate_Scan_Sequence.png" alt="HCI propagate scan sequence diagram"/></p>
