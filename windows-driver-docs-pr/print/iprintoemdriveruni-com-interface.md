---
title: IPrintOemDriverUni COM 接口
description: IPrintOemDriverUni COM 接口
ms.assetid: 84b3f43c-039a-4e9d-b596-41c08f1e0284
keywords:
- IPrintOemDriverUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95e04b3ac99b8e3dc00017b64f1e60f1edb327ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521213"
---
# <a name="iprintoemdriveruni-com-interface"></a>IPrintOemDriverUni COM 接口





`IPrintOemDriverUni COM`接口提供了有权访问为 Unidrv 通过打印机图形 DLL 提供的实用程序操作插件的呈现。 这些操作数据流发送到打印后台处理程序，并获取驱动程序管理信息。

下表列出并描述所有定义的方法**IPrintOemDriverUni**接口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553126" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553126)"><strong>IPrintOemDriverUni::DrvGetDriverSetting</strong></a></p></td>
<td><p>返回打印机功能和其他内部信息的当前的状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553128" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553128)"><strong>IPrintOemDriverUni::DrvGetGPDData</strong></a></p></td>
<td><p>使呈现插件来获取在打印机中定义的数据&#39;s <a href="https://msdn.microsoft.com/library/windows/hardware/ff556283#wdkgloss-generic-printer-description--gpd-" data-raw-source="&lt;em&gt;generic printer description (GPD)&lt;/em&gt;"><em>通用打印机说明 (GPD)</em> </a>文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553129" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553129)"><strong>IPrintOemDriverUni::DrvGetStandardVariable</strong></a></p></td>
<td><p>使呈现插件获取 Unidrv 的当前值&#39;s<a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">标准变量</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553132" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvUniTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553132)"><strong>IPrintOemDriverUni::DrvUniTextOut</strong></a></p></td>
<td><p>允许呈现插件使用设备管理的绘图图面以轻松地输出文本字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553135" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteAbortBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553135)"><strong>IPrintOemDriverUni::DrvWriteAbortBuf</strong></a></p></td>
<td><p>允许呈现插件，以重置打印机后用户已终止打印作业。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553138" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteSpoolBuf&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553138)"><strong>IPrintOemDriverUni::DrvWriteSpoolBuf</strong></a></p></td>
<td><p>将打印机数据发送到后台处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553141" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvXMoveTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553141)"><strong>IPrintOemDriverUni::DrvXMoveTo</strong></a></p></td>
<td><p>通知 Unidrv 光标的 x 位置更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553144" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvYMoveTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553144)"><strong>IPrintOemDriverUni::DrvYMoveTo</strong></a></p></td>
<td><p>通知 Unidrv 光标 y 位置发生变化。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




