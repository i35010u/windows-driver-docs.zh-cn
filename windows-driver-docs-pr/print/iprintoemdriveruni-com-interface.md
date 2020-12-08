---
title: IPrintOemDriverUni COM 接口
description: IPrintOemDriverUni COM 接口
keywords:
- IPrintOemDriverUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0b8e407f592a9fd7810f170bda1f83d5f7dfa71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796562"
---
# <a name="iprintoemdriveruni-com-interface"></a>IPrintOemDriverUni COM 接口





`IPrintOemDriverUni COM`接口提供了一个呈现插件，其中包含对 Unidrv 的打印机图形 DLL 提供的实用工具操作的访问。 这些操作将数据流发送到打印后台处理程序，并获取驱动程序管理的信息。

下表列出并描述了 **IPrintOemDriverUni** 接口定义的所有方法。

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
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetDriverSetting&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetdriversetting)"><strong>IPrintOemDriverUni：:D rvGetDriverSetting</strong></a></p></td>
<td><p>返回打印机功能和其他内部信息的当前状态。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetGPDData&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetgpddata)"><strong>IPrintOemDriverUni：:D rvGetGPDData</strong></a></p></td>
<td><p>启用呈现插件以获取打印机 <a href="/windows-hardware/drivers/#wdkgloss-generic-printer-description--gpd-" data-raw-source="&lt;em&gt;generic printer description (GPD)&lt;/em&gt;"><em>一般打印机说明 (GPD) </em></a> 文件中定义的数据。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvGetStandardVariable&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvgetstandardvariable)"><strong>IPrintOemDriverUni：:D rvGetStandardVariable</strong></a></p></td>
<td><p>启用呈现插件以获取 Unidrv 的 <a href="standard-variables.md" data-raw-source="[standard variables](standard-variables.md)">标准变量</a>的当前值。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvUniTextOut&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)"><strong>IPrintOemDriverUni：:D rvUniTextOut</strong></a></p></td>
<td><p>启用使用设备托管的绘图图面的呈现插件来轻松输出文本字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwriteabortbuf" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteAbortBuf&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwriteabortbuf)"><strong>IPrintOemDriverUni：:D rvWriteAbortBuf</strong></a></p></td>
<td><p>允许呈现插件在用户终止打印作业后重置打印机。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvWriteSpoolBuf&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvwritespoolbuf)"><strong>IPrintOemDriverUni：:D rvWriteSpoolBuf</strong></a></p></td>
<td><p>将打印机数据发送到后台处理程序。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvXMoveTo&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvxmoveto)"><strong>IPrintOemDriverUni：:D rvXMoveTo</strong></a></p></td>
<td><p>通知 Unidrv 光标 x 位置的更改。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto" data-raw-source="[&lt;strong&gt;IPrintOemDriverUni::DrvYMoveTo&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemdriveruni-drvymoveto)"><strong>IPrintOemDriverUni：:D rvYMoveTo</strong></a></p></td>
<td><p>向 Unidrv 通知游标的 y 位置更改。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

