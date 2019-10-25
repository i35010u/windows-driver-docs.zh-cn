---
title: 智能卡驱动程序库回调例程
description: 智能卡驱动程序库回调例程
ms.assetid: e536d539-4871-4b1d-bb5a-92a310dfa1e7
keywords:
- IOCTLs WDK 智能卡
- 库回调例程 WDK 智能卡
- 回调例程 WDK 智能卡
- ReaderFunction
- 供应商提供的驱动程序 WDK 智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19a3b6db0d38847219a1de4bf220ada0ddbb876e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845046"
---
# <a name="smart-card-driver-library-callback-routines"></a>智能卡驱动程序库回调例程


## <span id="_ntovr_smart_card_driver_library_callback_routines"></span><span id="_NTOVR_SMART_CARD_DRIVER_LIBRARY_CALLBACK_ROUTINES"></span>


智能卡体系结构定义一组标准回调例程类型。 有关这些例程的详细信息，请参阅[智能卡驱动程序回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

读取器驱动程序必须将这些回调例程提供给驱动程序库例程[**SmartcardDeviceControl （WDM）** ](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))，以便通过在智能卡设备扩展中存储指向它们的指针（这是智能卡[ **\_扩展**](https://docs.microsoft.com/windows-hardware/drivers/ddi/smclib/ns-smclib-_smartcard_extension)类型）来调用。 这些指针存储在智能卡\_扩展结构的**ReaderFunction**成员中的数组中。 单个回调例程可以通过一系列常数值标识，这些值应用作**ReaderFunction**数组中的索引。

例如，如果想要[**SmartcardDeviceControl**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))在读取器驱动程序处理[**IOCTL\_智能卡\_POWER**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548907(v=vs.85)) request 后，调用该程序中名为**DriverCardPower**的回调例程，则必须使用[*RDF\_卡\_POWER*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))常量，按以下方式初始化设备扩展：

```cpp
SmartcardExtension->ReaderFunction[RDF_CARD_POWER] = 
DriverCardPower;
```

RDF\_卡\_电源是固定的系统定义的常量，始终对应于服务于 IOCTL\_智能卡\_POWER request 的回调例程。

如果与正在处理的 IOCTL 相对应的**ReaderFunction**数组的成员为**NULL**，则[**SmartcardDeviceControl**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))将返回状态状态\_不\_支持读取器驱动程序。 在某些情况下，此行为很有用。 例如，如果您的驱动程序不支持卡弹出或卡抑制，只需将**ReaderFunction**数组的相应成员分配为**NULL**， **SMARTCARDDEVICECONTROL**将返回状态\_不\_只要调用此成员例程，就支持。

下表列出了用于标识各种类型的回调例程的常量。 这些是应用作**ReaderFunction**数组索引的常量。 该表还提供了每个例程类型的简短描述，并指示读取器驱动程序是否必需或可选以便实现例程。

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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_POWER&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548919(v=vs.85))"><em>RDF_CARD_POWER</em></a></p></td>
<td align="left"><p>重置或关闭插入的智能卡</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_EJECT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548918(v=vs.85))"><em>RDF_CARD_EJECT</em></a></p></td>
<td align="left"><p>弹出插入的智能卡</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_CARD_TRACKING&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))"><em>RDF_CARD_TRACKING</em></a></p></td>
<td align="left"><p>安装事件处理程序以跟踪卡的插入和删除</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_IOCTL_VENDOR&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548921(v=vs.85))"><em>RDF_IOCTL_VENDOR</em></a></p></td>
<td align="left"><p>执行特定于供应商的 IOCTL 操作</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_READER_SWALLOW&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548922(v=vs.85))"><em>RDF_READER_SWALLOW</em></a></p></td>
<td align="left"><p>机械吞并</p></td>
<td align="left"><p>可选</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_SET_PROTOCOL&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548923(v=vs.85))"><em>RDF_SET_PROTOCOL</em></a></p></td>
<td align="left"><p>为卡读卡器中的卡选择传输协议</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85)" data-raw-source="[&lt;em&gt;RDF_TRANSMIT&lt;/em&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548924(v=vs.85))"><em>RDF_TRANSMIT</em></a></p></td>
<td align="left"><p>执行数据传输</p></td>
<td align="left"><p>Mandatory</p></td>
</tr>
</tbody>
</table>

 

当读取器驱动程序调用这些例程时，它应从输入缓冲区中检索调用参数，如[智能卡驱动程序回调](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)中所述。 读取器驱动程序还应将输出数据存储在相应的缓冲区区域，如同一节中所述。

当卡跟踪回调例程以外的任何回调例程返回状态\_"挂起" 时，智能卡库将停止处理来自读取器驱动程序的任何进一步调用。 （有关卡跟踪回调例程的信息，请参阅[*RDF\_卡\_跟踪*](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548920(v=vs.85))。）如果读取器驱动程序在库处于此状态时尝试使用驱动程序库例程，则库例程返回状态\_设备\_繁忙状态。 这会有效地阻止读取器驱动程序从资源管理器处理 IOCTL 请求，因为如果读取器驱动程序无法调用[**SmartcardDeviceControl**](https://docs.microsoft.com/previous-versions/ff548939(v=vs.85))，则它无法处理 ioctl 请求。

 

 





