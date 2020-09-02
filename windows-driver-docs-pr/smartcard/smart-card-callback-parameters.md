---
title: 智能卡回调参数
description: 智能卡回调参数
ms.assetid: 6fd1590b-0600-4065-b1cc-71d8aed3f98a
keywords:
- IOCTLs WDK 智能卡
- 回拨参数 WDK 智能卡
- 供应商提供的驱动程序 WDK 智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9c5a6b164174379317b5a80ba1a75f605017d30
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381351"
---
# <a name="smart-card-callback-parameters"></a>智能卡回调参数


## <span id="_ntovr_smart_card_callback_parameters"></span><span id="_NTOVR_SMART_CARD_CALLBACK_PARAMETERS"></span>


对于除[** \_ \_ \_ 缺少 ioctl 智能卡**](/previous-versions/windows/hardware/drivers/ff548905(v=vs.85))之外的所有 ioctl 请求和[**IOCTL \_ 智能卡 \_ \_ **](/previous-versions/windows/hardware/drivers/ff548906(v=vs.85))， [**SmartcardDeviceControl (WDM) **](/previous-versions/ff548939(v=vs.85))在调用回调例程之前初始化[**智能卡 \_ 扩展**](/windows-hardware/drivers/ddi/smclib/ns-smclib-_smartcard_extension)结构的**IoRequest**成员。 下表指明了 **SmartcardDeviceControl** 执行的初始化的种类。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IoRequest 的成员</th>
<th align="left">SmartcardDeviceControl 执行的初始化</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IoRequest.RequestBuffer</strong></p></td>
<td align="left"><p>存储要发送到此成员指向的缓冲区中的卡的用户数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.RequestBufferLength</strong></p></td>
<td align="left"><p>在此成员中存储用户缓冲区的长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest.ReplyBuffer</strong></p></td>
<td align="left"><p>将智能卡返回的数据存储在此成员指向的缓冲区中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.ReplyBufferLength</strong></p></td>
<td align="left"><p>将答复缓冲区的大小存储在此成员中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest 信息</strong></p></td>
<td align="left"><p>存储在此成员指向的变量中实际收到的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MajorIoControlCode</strong></p></td>
<td align="left"><p>将 IOCTL 请求的主要 i/o 控制代码存储在此成员中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MinorIoControlCode</strong></p></td>
<td align="left"><p>如果此成员中的 IOCTL 请求的任何) ，则存储次 i/o 控制代码 (。</p></td>
</tr>
</tbody>
</table>

 

按下表所述设置 **SmartcardExtension- &gt; OsData** 指向的结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>CurrentIrp</strong></p></td>
<td align="left"><p>接收一个指针，该指针指向每个控制请求的请求 IRP （ <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548905(v=vs.85)" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_ABSENT&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff548905(v=vs.85))"><strong>IOCTL_SMARTCARD_IS_ABSENT</strong></a> 和 <a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548906(v=vs.85)" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_PRESENT&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff548906(v=vs.85))"><strong>IOCTL_SMARTCARD_IS_PRESENT</strong></a>除外）。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NotificationIrp</strong></p></td>
<td align="left"><p>接收一个指针，该指针指向 IOCTL_SMARTCARD_IS_ABSENT 的请求 IRP 或 IOCTL_SMARTCARD_IS_PRESENT 控制请求。</p></td>
</tr>
</tbody>
</table>

 

 

