---
Description: 支持自动播放
title: 支持自动播放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae2236bccd98008dadffbb349c988caac1e65c42
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464090"
---
# <a name="supporting-autoplay"></a>支持自动播放


自动播放功能的外壳程序检测到便携设备上的内容。 根据当前的自动播放设置，此功能将执行以下某项操作，例如显示可用的处理程序应用程序，显示文件的标准文件夹视图的列表，依此类推。

在 Windows Vista 中，自动播放功能已扩展，以便 WPD 设备可以向它支持的内容类型的列表。 同样，WPD 应用程序可以注册它们支持的内容类型。 （有关注册应用程序的详细信息，请参阅 WPD SDK）。

## <a name="span-idthewpdautoplayschemespanspan-idthewpdautoplayschemespanspan-idthewpdautoplayschemespanthe-wpd-autoplay-scheme"></a><span id="The_WPD_AutoPlay_Scheme"></span><span id="the_wpd_autoplay_scheme"></span><span id="THE_WPD_AUTOPLAY_SCHEME"></span>WPD 自动播放方案


与 Windows Vista 自动播放功能集成，WPD 自动播放方案。 它会通过支持以下表所述的三个自动播放类别。

| 类别 | 描述                                                                                                         |
|----------|---------------------------------------------------------------------------------------------------------------------|
| 源   | WPD 设备可将其视为内容的源，即，从设备传输内容。        |
| 接收器     | WPD 设备可将其视为内容的目标，也就是说，内容可以传输到设备。    |
| 函数 | WPD 设备支持可编程或可控制功能，例如，它可以发送和接收 SMS 消息。 |

 

支持这些类别的设备应在设备中设置的相应条目\_AddReg 部分中的安装程序信息 (.inf) 文件。 下表列出了 WPD 类安装程序支持的两个自动播放指令。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">部分</th>
<th align="left">指令或参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">AutoPlaySourceOnly</td>
<td align="left">此指令时要求仅充当自动播放源设备。
<ul>
<li>Reg 根必须是"HKR"。</li>
<li>类型必须为 0x10001。</li>
<li>必须设置的值为 1。</li>
</ul>
<p>例如：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"AutoPlaySourceOnly",0x10001,1</code></p></td>
</tr>
<tr class="even">
<td align="left">Device_AddReg</td>
<td align="left">EnableDefaultAutoPlaySupport directive</td>
<td align="left">此指令是必需的。
<ul>
<li>Reg 根必须是"HKR"。</li>
<li>类型必须为 0x10001。</li>
<li>必须设置有效的值 （0 或 1）。</li>
</ul>
<p>例如：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableDefaultAutoPlaySupport",0x10001,1</code></p></td>
</tr>
</tbody>
</table>

 

大多数设备将在其安装程序信息文件中指定 EnableDefaultAutoPlaySupport 指令。 仅适用于不支持的双向传输的旧设备提供 AutoPlaySourceOnly 指令。

如果不希望你的设备以参与自动播放，将 EnableAutoPlaySupport 指令设置为 0，或省略此指令从您的驱动程序安装程序信息 (.inf) 文件。 如果需要显式禁用任何给定 WPD 设备的自动播放功能，就可以做到在设备中创建值为 false DeviceHandlers\_.inf 文件的参数部分。

如果需要创建自定义的自动播放方案，就可以做到在设备中创建一个专用的 DeviceHandlers 值\_参数部分中的安装程序信息 (.inf) 文件。

 

 




