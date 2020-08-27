---
description: 支持自动播放
title: 支持自动播放
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00c3d9f1fc337df93df8ed66837447239d702181
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969152"
---
# <a name="supporting-autoplay"></a>支持自动播放


自动播放是 Shell 的一项功能，可检测便携设备上的内容。 根据当前的 "自动播放" 设置，此功能将执行几个操作之一，例如显示可用处理程序应用程序的列表、显示文件的标准文件夹视图等。

在 Windows Vista 中，自动播放功能已扩展，因此 WPD 设备可以提供它所支持的内容类型列表。 同样，WPD 应用程序可以注册其支持的内容类型。  (有关注册应用程序的详细信息，请参阅 WPD SDK。 ) 

## <a name="span-idthe_wpd_autoplay_schemespanspan-idthe_wpd_autoplay_schemespanspan-idthe_wpd_autoplay_schemespanthe-wpd-autoplay-scheme"></a><span id="The_WPD_AutoPlay_Scheme"></span><span id="the_wpd_autoplay_scheme"></span><span id="THE_WPD_AUTOPLAY_SCHEME"></span>WPD 自动播放方案


WPD 自动播放方案与 Windows Vista 自动播放功能集成。 它通过支持三个自动播放类别来实现此目的，下表对此进行了介绍。

| 类别 | 说明                                                                                                         |
|----------|---------------------------------------------------------------------------------------------------------------------|
| 源   | 可以将 WPD 设备视为内容源，即，可以从设备传输内容。        |
| 接收器     | 可以将 WPD 设备视为内容的目标，也就是说，可以将内容传输到设备。    |
| 函数 | WPD 设备支持可编程或可控制的功能，例如，它可以发送和接收短信。 |

 

支持这些类别的设备应在 \_ setup information ( .inf) file 的 Device AddReg 部分中设置相应的条目。 下表列出了 WPD 类安装程序支持的两个自动播放指令。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Device_AddReg</td>
<td align="left">AutoPlaySourceOnly</td>
<td align="left">仅充当自动播放源的设备需要此指令。
<ul>
<li>注册表根必须是 "HKR"。</li>
<li>类型必须为0x10001。</li>
<li>必须设置值1。</li>
</ul>
<p>示例：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"AutoPlaySourceOnly",0x10001,1</code></p></td>
</tr>
<tr class="even">
<td align="left">Device_AddReg</td>
<td align="left">EnableDefaultAutoPlaySupport 指令</td>
<td align="left">此指令是必需的。
<ul>
<li>注册表根必须是 "HKR"。</li>
<li>类型必须为0x10001。</li>
<li>必须设置 (0 或 1) 有效的值。</li>
</ul>
<p>示例：</p>
<p><code>[Device_AddReg]</code></p>
<p><code>HKR,,"EnableDefaultAutoPlaySupport",0x10001,1</code></p></td>
</tr>
</tbody>
</table>

 

大多数设备会在其安装信息文件中指定 EnableDefaultAutoPlaySupport 指令。 仅为不支持双向传输的旧设备提供 AutoPlaySourceOnly 指令。

如果你不希望你的设备参与自动播放，请将 EnableAutoPlaySupport 指令设置为0，或者从驱动程序的安装 ( 信息) 文件中省略此指令。 如果你明确需要对给定的 WPD 设备禁用任何自动播放功能，则可以通过在 .inf 文件的 "设备参数" 部分中创建 false DeviceHandlers 值来实现此目的 \_ 。

如果需要创建自定义自动播放方案，可以通过在 \_ "安装信息 ( .inf) 文件的" 设备参数 "部分中创建专用 DeviceHandlers 值来实现。

 

 




