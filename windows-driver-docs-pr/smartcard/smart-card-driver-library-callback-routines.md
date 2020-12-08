---
title: 智能卡驱动程序库回调例程
description: 智能卡驱动程序库回调例程
keywords:
- IOCTLs WDK 智能卡
- 库回调例程 WDK 智能卡
- 回调例程 WDK 智能卡
- ReaderFunction
- 供应商提供的驱动程序 WDK 智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e74f1c8245ace4b3929e5b900cb9a86e2b9d7616
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804881"
---
# <a name="smart-card-driver-library-callback-routines"></a>智能卡驱动程序库回调例程


## <span id="_ntovr_smart_card_driver_library_callback_routines"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY_CALLBACK_ROUTINES"></span>


智能卡体系结构定义一组标准回调例程类型。 有关这些例程的详细信息，请参阅 [智能卡驱动程序回调](/windows-hardware/drivers/ddi/index)。

读取器驱动程序必须通过在智能卡设备扩展中存储指向它们的指针（这是智能卡 [**\_ 扩展**](/windows-hardware/drivers/ddi/smclib/ns-smclib-_smartcard_extension)类型），使这些回调例程可供驱动程序库例程（ [**SmartcardDeviceControl (WDM)**](/previous-versions/ff548939(v=vs.85))使用。 这些指针存储在智能卡扩展结构的 **ReaderFunction** 成员中的数组中 \_ 。 单个回调例程可以通过一系列常数值标识，这些值应用作 **ReaderFunction** 数组中的索引。

例如，如果你想要 [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85))在处理 [**IOCTL \_ 智能卡 \_ 电源**](/previous-versions/windows/hardware/drivers/ff548907(v=vs.85))请求后，在名为 **DriverCardPower** 的读取器驱动程序中调用回调例程，则必须使用 [*RDF \_ 卡 \_ 电源*](/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))常量按以下方式初始化设备扩展：

```cpp
SmartcardExtension->ReaderFunction[RDF_CARD_POWER] = 
DriverCardPower;
```

RDF \_ 卡 \_ 电源是固定的系统定义的常量，始终对应于服务于 IOCTL \_ 智能卡电源请求的回调例程 \_ 。

如果与正在处理的 IOCTL 相对应的 **ReaderFunction** 数组的成员为 **NULL**，则 [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85)) 将返回 \_ \_ 读取器驱动程序不支持的状态状态。 在某些情况下，此行为很有用。 例如，如果您的驱动程序不支持卡弹出或卡抑制，只需将 **ReaderFunction** 数组的相应成员分配为 **NULL**，并且在调用该成员例程时， **SmartcardDeviceControl** 将返回 \_ 不 \_ 受支持的状态。

下表列出了用于标识各种类型的回调例程的常量。 这些是应用作 **ReaderFunction** 数组索引的常量。 该表还提供了每个例程类型的简短描述，并指示读取器驱动程序是否必需或可选以便实现例程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">相应回调例程的说明</th>
<th align="left">由读取器驱动程序实现</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548919(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_POWER&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))"><em>RDF_CARD_POWER</em></a></p></td>
<td align="left"><p>重置或关闭插入的智能卡</p></td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548918(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_EJECT&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548918(v=vs.85))"><em>RDF_CARD_EJECT</em></a></p></td>
<td align="left"><p>弹出插入的智能卡</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548920(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_TRACKING&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))"><em>RDF_CARD_TRACKING</em></a></p></td>
<td align="left"><p>安装事件处理程序以跟踪卡的插入和删除</p></td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548921(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_IOCTL_VENDOR&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548921(v=vs.85))"><em>RDF_IOCTL_VENDOR</em></a></p></td>
<td align="left"><p>执行特定于供应商的 IOCTL 操作</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548922(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_READER_SWALLOW&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548922(v=vs.85))"><em>RDF_READER_SWALLOW</em></a></p></td>
<td align="left"><p>机械吞并</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548923(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_SET_PROTOCOL&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548923(v=vs.85))"><em>RDF_SET_PROTOCOL</em></a></p></td>
<td align="left"><p>为卡读卡器中的卡选择传输协议</p></td>
<td align="left"><p>必需</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff548924(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_TRANSMIT&lt;/em&gt;](/previous-versions/windows/hardware/drivers/ff548924(v=vs.85))"><em>RDF_TRANSMIT</em></a></p></td>
<td align="left"><p>执行数据传输</p></td>
<td align="left"><p>必需</p></td>
</tr>
</tbody>
</table>

 

当读取器驱动程序调用这些例程时，它应从输入缓冲区中检索调用参数，如 [智能卡驱动程序回调](/windows-hardware/drivers/ddi/index)中所述。 读取器驱动程序还应将输出数据存储在相应的缓冲区区域，如同一节中所述。

当任何回调例程（而不是智能卡跟踪回调例程）返回 "挂起" 状态时 \_ ，智能卡库将停止处理来自读取器驱动程序的任何进一步调用。  (有关卡跟踪回调例程的信息，请参阅 [*RDF \_ 纸牌 \_ 跟踪*](/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))) 。如果读取器驱动程序在此状态下尝试使用驱动程序库例程，则库例程返回状态 \_ 设备繁忙状态 \_ 。 这会有效地阻止读取器驱动程序从资源管理器处理 IOCTL 请求，因为如果读取器驱动程序无法调用 [**SmartcardDeviceControl**](/previous-versions/ff548939(v=vs.85))，则它无法处理 ioctl 请求。

