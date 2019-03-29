---
title: 智能卡回调参数
description: 智能卡回调参数
ms.assetid: 6fd1590b-0600-4065-b1cc-71d8aed3f98a
keywords:
- Ioctl WDK 智能卡
- 回调参数 WDK 智能卡
- 供应商提供的驱动程序 WDK 的智能卡，IOCTL 请求管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a18240c2f97c7af4ecb7300f5de3c91f4cd8377
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563610"
---
# <a name="smart-card-callback-parameters"></a>智能卡回调参数


## <span id="_ntovr_smart_card_callback_parameters"></span><span id="_NTOVR_SMART_CARD_CALLBACK_PARAMETERS"></span>


对于所有 IOCTL 请求除外[ **IOCTL\_智能卡\_IS\_ABSENT** ](https://msdn.microsoft.com/library/windows/hardware/ff548905)并[ **IOCTL\_智能卡\_是\_存在**](https://msdn.microsoft.com/library/windows/hardware/ff548906)， [ **SmartcardDeviceControl (WDM)** ](https://msdn.microsoft.com/library/windows/hardware/ff548939)初始化**IoRequest**的成员[**智能卡\_扩展**](https://msdn.microsoft.com/library/windows/hardware/ff548974)结构之前调用回调例程。 下表指示初始化类的**SmartcardDeviceControl**执行。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IoRequest 的成员</th>
<th align="left">执行由 SmartcardDeviceControl 初始化</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IoRequest.RequestBuffer</strong></p></td>
<td align="left"><p>存储用户数据发送到此成员指向的缓冲区中的卡。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.RequestBufferLength</strong></p></td>
<td align="left"><p>此成员中存储用户缓冲区的长度。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest.ReplyBuffer</strong></p></td>
<td align="left"><p>将存储返回此成员指向的缓冲区中的智能卡的数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IoRequest.ReplyBufferLength</strong></p></td>
<td align="left"><p>此成员中存储回复缓冲区的大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IoRequest.Information</strong></p></td>
<td align="left"><p>将存储此成员指向的变量中的卡从实际接收到的字节数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MajorIoControlCode</strong></p></td>
<td align="left"><p>此成员中存储 IOCTL 请求主要的 I/O 控制的代码。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MinorIoControlCode</strong></p></td>
<td align="left"><p>此成员中存储 IOCTL 请求的次要 I/O 控制代码 （如果有）。</p></td>
</tr>
</tbody>
</table>

 

指向结构**SmartcardExtension-&gt;OsData**下表中所述设置。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>CurrentIrp</strong></p></td>
<td align="left"><p>接收指向请求的每个控件请求除 IRP <a href="https://msdn.microsoft.com/library/windows/hardware/ff548905" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_ABSENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548905)"> <strong>IOCTL_SMARTCARD_IS_ABSENT</strong> </a>并<a href="https://msdn.microsoft.com/library/windows/hardware/ff548906" data-raw-source="[&lt;strong&gt;IOCTL_SMARTCARD_IS_PRESENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548906)"> <strong>IOCTL_SMARTCARD_IS_PRESENT</strong> </a>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>NotificationIrp</strong></p></td>
<td align="left"><p>接收指向请求 IRP IOCTL_SMARTCARD_IS_ABSENT 或 IOCTL_SMARTCARD_IS_PRESENT 控制请求。</p></td>
</tr>
</tbody>
</table>

 

 

 





