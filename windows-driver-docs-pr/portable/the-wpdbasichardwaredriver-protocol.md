---
description: WpdBasicHardwareDriver 协议
title: WpdBasicHardwareDriver 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d55dbc02da471068f53615af147202801210b84d
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969348"
---
# <a name="the-wpdbasichardwaredriver-protocol"></a>WpdBasicHardwareDriver 协议


WpdBasicHardwareDriver 示例驱动程序支持一种简单的协议，其中包括设备标识符、数据包大小和传感器数据。 协议为由可编程微控制器传输并由示例驱动程序接收的传感器数据定义基本数据格式。 示例驱动程序分析数据包，并将其转换为 WPD 应用程序收到的自定义 WPD 事件。

安装设备和示例驱动程序之后，可以使用随 Windows 驱动程序工具包附带的 WpdMon 工具来查看此数据的数据包 (WDK) 。 此工具监视 WPD 驱动程序和 WPD API 之间 (WPD 命令和事件) 的流量。 以下屏幕截图显示了作为自定义 WPD 事件从驱动程序传输到 API 的 Sensiron 温度和湿度传感器的传感器数据。 自定义事件 GUID 由 *stdafx.h*中的 WpdBasicHardwareDriver 定义。

```ManagedCPlusPlus
DEFINE_GUID (EVENT_SENSOR_READING_UPDATED, 0xada23b0b, 0xce13, 0x4e11, 0x9d, 0x2f, 0x15, 0xfe, 0x10, 0xd6, 0x63, 0x37);
```

![wpd 监视器](images/wpdmon.png)

**注意**   传感器 \_ 读数和传感器 \_ 更新 \_ 间隔事件参数不是 WPD 架构的一部分。 需要编辑 WpdInfo 属性文件，以添加以下条目。  (如果未添加这些项，WpdMon 和 WpdInfo 工具将显示原始 PROPERTYKEYs，而不是友好名称。 ) 

 

```cpp
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

在上图中，传感器 \_ 读取行包含传感器使用 WPD API 发送的数据。 此数据是一个多字节数据包，其格式如下图所示：

![传感器数据包](images/sensiron_packetvsd.png)

第一个字节标识传感器，第二个字节指定元素的计数，第三个指定元素的大小，第四个到 (第四个和第四个计数) 字节包含实际数据元素，最后六个字节指定传感器将其数据发布到计算机的时间间隔。

这七个字节的元素数据指示当前温度为72.6 华氏度，而相对湿度为32.8%。 间隔数据的五个字节表示传感器每2000毫秒向计算机传输数据 (或每隔两秒钟) 。

下表指定了视差传感器示例工具包中的每个9个传感器的数据包格式。

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
<th align="left">传感器</th>
<th align="left">传感器 ID</th>
<th align="left">元素计数</th>
<th align="left">元素大小</th>
<th align="left">元素</th>
<th align="left">时间间隔</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">指南针</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">3</td>
<td align="left">标题 (3 个字节) </td>
<td align="left">6个字节</td>
</tr>
<tr class="even">
<td align="left">Sensiron</td>
<td align="left">2</td>
<td align="left">1</td>
<td align="left">7</td>
<td align="left">Temp (4 个字节) 
<p>湿度 (3 个字节) </p></td>
<td align="left">6个字节</td>
</tr>
<tr class="odd">
<td align="left">弹性力</td>
<td align="left">3</td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left">强制 (5 字节) </td>
<td align="left">6个字节</td>
</tr>
<tr class="even">
<td align="left">Ultrasonic Ping</td>
<td align="left">4</td>
<td align="left">1</td>
<td align="left">5</td>
<td align="left"> (为5字节的距离) </td>
<td align="left">6个字节</td>
</tr>
<tr class="odd">
<td align="left">被动红外线</td>
<td align="left">5</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">状态 (1 个字节) </td>
<td align="left">6个字节</td>
</tr>
<tr class="even">
<td align="left">Memsic</td>
<td align="left">6</td>
<td align="left">1</td>
<td align="left">8</td>
<td align="left">x 轴 G (4 个字节) 
<p>y 轴 G (4 个字节) </p></td>
<td align="left">6个字节</td>
</tr>
<tr class="odd">
<td align="left">QTI</td>
<td align="left">7</td>
<td align="left">1</td>
<td align="left">4</td>
<td align="left">轻型度量 (4 个字节) </td>
<td align="left">6个字节</td>
</tr>
<tr class="even">
<td align="left">Piezo 振动</td>
<td align="left">8</td>
<td align="left">1</td>
<td align="left">1</td>
<td align="left">状态 (1 个字节) </td>
<td align="left">6个字节</td>
</tr>
<tr class="odd">
<td align="left">架式</td>
<td align="left">9</td>
<td align="left">3</td>
<td align="left">4</td>
<td align="left">x 轴 G (4 个字节) 
<p>y 轴 G (4 个字节) </p>
<p>z 轴 G (4 个字节) </p></td>
<td align="left">6个字节</td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





