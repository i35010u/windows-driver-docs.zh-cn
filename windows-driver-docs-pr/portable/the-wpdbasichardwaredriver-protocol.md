---
Description: The WpdBasicHardwareDriver Protocol
title: WpdBasicHardwareDriver 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a53dc95edb3b90acd1a56727ac6fdd2ac19ae24
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562617"
---
# <a name="the-wpdbasichardwaredriver-protocol"></a>WpdBasicHardwareDriver 协议


WpdBasicHardwareDriver 示例驱动程序支持一种简单协议，包括设备标识符、 数据包大小和传感器数据。 该协议定义传输的可编程微控制器和接收的示例驱动程序的传感器数据的基本数据格式。 示例驱动程序分析的数据包，并将其转换成 WPD 应用程序接收的自定义 WPD 事件。

安装设备的示例驱动程序后，可以使用附带的 WpdMon 工具使用 Windows Driver Kit (WDK) 中查看此数据的数据包。 该工具通过监视 WPD 驱动程序和 WPD API 之间的流量 （WPD 命令和事件）。 以下屏幕截图显示正在从传输驱动程序到 API 作为自定义 WPD 事件 Sensiron 温度和湿度传感器的传感器数据。 自定义事件 GUID 定义由在 WpdBasicHardwareDriver *Stdafx.h*。

```ManagedCPlusPlus
DEFINE_GUID (EVENT_SENSOR_READING_UPDATED, 0xada23b0b, 0xce13, 0x4e11, 0x9d, 0x2f, 0x15, 0xfe, 0x10, 0xd6, 0x63, 0x37);
```

![wpd 监视器](images/wpdmon.png)

**请注意**  传感器\_读取和传感器\_更新\_间隔事件参数不是 WPD 架构的一部分。 它有必要编辑 WpdInfo 属性文件，添加以下条目。 （如果未添加这些项，WpdMon 和 WpdInfo 工具将显示原始 PROPERTYKEYs 而不是友好名称。）

 

```cpp
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

在上一图中，传感器\_读取一行包含使用 WPD api 驱动程序发送的传感器数据。 此数据是多字节的数据包，格式如下图中所示：

![传感器数据包](images/sensiron_packetvsd.png)

第一个字节标识传感器、 第二个指定的元素计数、 第三个指定的元素的大小、 通过 （第四个 + 计数） 的第四个字节包含实际数据元素和最后六个字节指定的时间间隔传感器将其数据发布到计算机。

元素数据的七个字节表示当前温度是 72.6 华氏度相对湿度是 32.8%。 五个字节的时间间隔数据指示传感器传输到计算机的数据，每隔 2,000 毫秒 （或每两秒）。

下表为每个九个传感器视差传感器示例工具包中找到的指定数据包格式。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Sensor</th>
<th align="left">传感器 ID</th>
<th align="left">元素计数</th>
<th align="left">元素大小</th>
<th align="left">元素</th>
<th align="left">间隔</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">指南针</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left">标题 （3 个字节）</td>
<td align="left">6 个字节</td>
</tr>
<tr class="even">
<td align="left">Sensiron</td>
<td align="left">2</td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left">Temp （4 字节）
<p>湿度 （3 个字节）</p></td>
<td align="left">6 个字节</td>
</tr>
<tr class="odd">
<td align="left">弹性强制</td>
<td align="left">3</td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left">强制 （5 个字节）</td>
<td align="left">6 个字节</td>
</tr>
<tr class="even">
<td align="left">Ultrasonic Ping</td>
<td align="left">4</td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left">距离 （5 个字节）</td>
<td align="left">6 个字节</td>
</tr>
<tr class="odd">
<td align="left">被动红外</td>
<td align="left">5</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">状态 （1 个字节）</td>
<td align="left">6 个字节</td>
</tr>
<tr class="even">
<td align="left">Memsic</td>
<td align="left">6</td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left">x 轴 G （4 字节）
<p>y 轴 G （4 字节）</p></td>
<td align="left">6 个字节</td>
</tr>
<tr class="odd">
<td align="left">QTI</td>
<td align="left">7</td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left">浅度量 （4 字节）</td>
<td align="left">6 个字节</td>
</tr>
<tr class="even">
<td align="left">Piezo 振动</td>
<td align="left">8</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">状态 （1 个字节）</td>
<td align="left">6 个字节</td>
</tr>
<tr class="odd">
<td align="left">人： Hitachi</td>
<td align="left">9</td>
<td align="left">3</td>
<td align="left">4</td>
<td align="left">x 轴 G （4 字节）
<p>y 轴 G （4 字节）</p>
<p>z 轴 G （4 字节）</p></td>
<td align="left">6 个字节</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





