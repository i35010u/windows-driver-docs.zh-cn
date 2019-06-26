---
title: 智能卡驱动程序库回调例程
description: 智能卡驱动程序库回调例程
ms.assetid: e536d539-4871-4b1d-bb5a-92a310dfa1e7
keywords:
- Ioctl WDK 智能卡
- 库回调例程 WDK 智能卡
- 回调例程 WDK 智能卡
- ReaderFunction
- 供应商提供的驱动程序 WDK 的智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74b6b2878385ebe9791d76ce702fa72e2b2bde77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356666"
---
# <a name="smart-card-driver-library-callback-routines"></a>智能卡驱动程序库回调例程


## <span id="_ntovr_smart_card_driver_library_callback_routines"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY_CALLBACK_ROUTINES"></span>


智能卡体系结构定义一的组标准的回调例程类型。 有关这些例程的详细信息，请参阅[智能卡驱动程序回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

读卡器驱动程序必须提供这些回调例程的驱动程序库例程[ **SmartcardDeviceControl (WDM)** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))，以通过将指向它们存储在智能卡设备扩展中，调用它属于类型[**智能卡\_扩展**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/smclib/ns-smclib-_smartcard_extension)。 这些指针存储在一个数组，其中位于**ReaderFunction**智能卡的成员\_扩展结构。 可以通过一系列的常量值，应将用作索引标识单个回调例程**ReaderFunction**数组。

例如，如果你想[ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))若要在名为你读卡器驱动程序中调用回调例程**DriverCardPower**每当完成处理[**IOCTL\_智能卡\_POWER** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548907(v=vs.85))请求，则必须使用[ *RDF\_卡\_POWER*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))常量，以按以下方式初始化设备扩展：

```cpp
SmartcardExtension->ReaderFunction[RDF_CARD_POWER] = 
DriverCardPower;
```

RDF\_卡\_电源是一个固定的系统定义的常量，它始终对应于服务 IOCTL 的回调例程\_智能卡\_POWER 请求。

如果的成员**ReaderFunction**数组，对应于正在处理 IOCTL 是**NULL**， [ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))返回的状态\_不\_到读卡器驱动程序支持。 在某些情况下，此行为很有用。 如果，例如，您的驱动程序不支持卡弹出或卡抑制，只需将指定的适当成员**ReaderFunction**数组**NULL**，和**SmartcardDeviceControl**将返回状态\_不\_成员例程称为每当受支持。

下表列出了标识的各种类型的回调例程的常量。 这些是应使用索引作为常量**ReaderFunction**数组。 表还提供了每个例程的类型的简要说明，并指示是否为必需或可选的读卡器驱动程序以实现的例程。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">索引</th>
<th align="left">相应的回调例程的说明</th>
<th align="left">要由读卡器驱动程序实现</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_POWER&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))"><em>RDF_CARD_POWER</em></a></p></td>
<td align="left"><p>重置或关闭插入的智能卡</p></td>
<td align="left"><p>强制</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_EJECT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85))"><em>RDF_CARD_EJECT</em></a></p></td>
<td align="left"><p>将弹出一个插入的智能卡</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_TRACKING&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))"><em>RDF_CARD_TRACKING</em></a></p></td>
<td align="left"><p>安装事件处理程序来跟踪卡插入和删除</p></td>
<td align="left"><p>强制</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_IOCTL_VENDOR&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85))"><em>RDF_IOCTL_VENDOR</em></a></p></td>
<td align="left"><p>执行特定于供应商 IOCTL 操作</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_READER_SWALLOW&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85))"><em>RDF_READER_SWALLOW</em></a></p></td>
<td align="left"><p>Does 机械理解</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_SET_PROTOCOL&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85))"><em>RDF_SET_PROTOCOL</em></a></p></td>
<td align="left"><p>选择卡读卡器中的卡的传输协议</p></td>
<td align="left"><p>强制</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_TRANSMIT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85))"><em>RDF_TRANSMIT</em></a></p></td>
<td align="left"><p>执行数据传输</p></td>
<td align="left"><p>强制</p></td>
</tr>
</tbody>
</table>

 

当读卡器驱动程序调用这些例程时，它应调用的参数从检索的输入缓冲区中所述[智能卡驱动程序回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。 读卡器驱动程序还应在适当的缓冲区的地区，存储输出数据，在相同节中所述。

当卡跟踪回调例程以外的任何回调例程返回状态\_挂起、 智能卡库将停止处理从读卡器驱动程序的任何进一步调用。 (有关卡跟踪回调例程的信息，请参阅[ *RDF\_卡\_跟踪*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))。)如果读卡器驱动程序尝试使用驱动程序库例程库处于此状态时，库例程将返回状态的状态\_设备\_忙。 这可有效地阻止读卡器驱动程序无法从资源管理器，IOCTL 请求提供服务因为读卡器驱动程序不能处理 IOCTL 请求，如果它不能调用[ **SmartcardDeviceControl** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85)).

 

 





