---
title: IPrintOemUni COM 接口
description: IPrintOemUni COM 接口
ms.assetid: b120def0-f270-49c6-b12f-10c220801f51
keywords:
- IPrintOemUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16bf418858515cd1a7957728cec77c67980b4bc3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90101644"
---
# <a name="iprintoemuni-com-interface"></a>IPrintOemUni COM 接口





`IPrintOemUni`COM 接口是 Unidrv 的[打印机图形 DLL](printer-graphics-dll.md)与呈现插件进行通信的方式。 `IPrintOemUni`接口由每个呈现插件实现。

下表列出并描述了接口提供的所有方法 `IPrintOemUni` 。 呈现插件必须定义所有列出的方法。 如果方法不是必需的，则可以只返回 E \_ NOTIMPL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-commandcallback)"><strong>IPrintOemUni::CommandCallback</strong></a></p></td>
<td><p>允许呈现插件提供动态生成的打印机命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression" data-raw-source="[&lt;strong&gt;IPrintOemUni::Compression&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression)"><strong>IPrintOemUni：： Compression</strong></a></p></td>
<td><p>允许呈现插件提供自定义的位图压缩方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-devmode" data-raw-source="[&lt;strong&gt;IPrintOemUni::DevMode&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-devmode)"><strong>IPrintOemUni：:D evMode</strong></a></p></td>
<td><p>对呈现插件的私有 DEVMODE 成员执行操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disabledriver" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisableDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disabledriver)"><strong>IPrintOemUni：:D isableDriver</strong></a></p></td>
<td><p>释放由呈现插件的 <strong>IPrintOemUni：： EnableDriver</strong> 方法分配的资源。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disablepdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisablePDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-disablepdev)"><strong>IPrintOemUni：:D isablePDEV</strong></a></p></td>
<td><p>允许呈现插件删除由其 <a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)"><strong>IPrintOemUni：： EnablePDEV</strong></a> 方法分配的私有 PDEV 结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadcharglyph" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadCharGlyph&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadcharglyph)"><strong>IPrintOemUni：:D ownloadCharGlyph</strong></a></p></td>
<td><p>允许呈现插件将指定软字体的字符标志符号下载到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadfontheader" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadFontHeader&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadfontheader)"><strong>IPrintOemUni：:D ownloadFontHeader</strong></a></p></td>
<td><p>允许使用呈现插件将字体的标题信息下载到打印机。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms" data-raw-source="[&lt;strong&gt;IPrintOemUni::DriverDMS&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-driverdms)"><strong>IPrintOemUni：:D riverDMS</strong></a></p></td>
<td><p>允许呈现插件指示它将使用设备托管的绘图图面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnableDriver&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)"><strong>IPrintOemUni::EnableDriver</strong></a></p></td>
<td><p>允许呈现插件挂钩某些图形 DDI 函数。 请注意，必须将此方法和 <strong>IPrintOemUni：:D isabledriver</strong> 视为成对的;如果实现了一个，则还必须实现另一个。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-enablepdev)"><strong>IPrintOemUni::EnablePDEV</strong></a></p></td>
<td><p>允许呈现插件创建其自己的 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics" data-raw-source="[&lt;strong&gt;IPrintOemUni::FilterGraphics&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-filtergraphics)"><strong>IPrintOemUni::FilterGraphics</strong></a></p></td>
<td><p>允许使用呈现插件来修改扫描行数据并将其发送到后台处理程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetImplementedMethod&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getimplementedmethod)"><strong>IPrintOemUni::GetImplementedMethod</strong></a></p></td>
<td><p>需要 (实现。 ) 允许 Unidrv 确定 <code>IPrintOemUni</code> 呈现插件已实现的接口方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetInfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-getinfo)"><strong>IPrintOemUni：： GetInfo</strong></a></p></td>
<td><p>需要 (实现。 ) 返回呈现插件的标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-halftonepattern)"><strong>IPrintOemUni::HalftonePattern</strong></a></p></td>
<td><p>允许呈现插件在半色调操作中使用半色调模式之前创建或修改它。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"><strong>IPrintOemUni::ImageProcessing</strong></a></p></td>
<td><p>允许使用呈现插件来修改图像位图数据，以便执行颜色格式设置或半色调。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage" data-raw-source="[&lt;strong&gt;IPrintOemUni::MemoryUsage&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-memoryusage)"><strong>IPrintOemUni：： MemoryUsage</strong></a></p></td>
<td><p>允许呈现插件指定其 <a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-imageprocessing)"><strong>IPrintOemUni：： ImageProcessing</strong></a> 方法使用所需的内存量。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-outputcharstr" data-raw-source="[&lt;strong&gt;IPrintOemUni::OutputCharStr&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-outputcharstr)"><strong>IPrintOemUni::OutputCharStr</strong></a></p></td>
<td><p>允许使用呈现插件控制字体标志符号的打印。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemUni::PublishDriverInterface&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-publishdriverinterface)"><strong>IPrintOemUni：:P ublishDriverInterface</strong></a></p></td>
<td><p>需要 (实现。 ) 提供指向 Unidrv 驱动程序的 <a href="iprintoemdriveruni-com-interface.md" data-raw-source="[IPrintOemDriverUni COM interface](iprintoemdriveruni-com-interface.md)">IPRINTOEMDRIVERUNI COM 接口</a> 或 <a href="/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni" data-raw-source="[IPrintCoreHelperUni interface](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)">IPrintCoreHelperUni 接口</a>的指针。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-resetpdev" data-raw-source="[&lt;strong&gt;IPrintOemUni::ResetPDEV&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-resetpdev)"><strong>IPrintOemUni::ResetPDEV</strong></a></p></td>
<td><p>允许呈现插件重置其 PDEV 结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-sendfontcmd" data-raw-source="[&lt;strong&gt;IPrintOemUni::SendFontCmd&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-sendfontcmd)"><strong>IPrintOemUni::SendFontCmd</strong></a></p></td>
<td><p>允许使用呈现插件来修改打印机的字体选择命令，然后将其发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap" data-raw-source="[&lt;strong&gt;IPrintOemUni::TextOutAsBitmap&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)"><strong>IPrintOemUni::TextOutAsBitmap</strong></a></p></td>
<td><p>允许呈现插件创建文本字符串的位图图像。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttdownloadmethod" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTDownloadMethod&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttdownloadmethod)"><strong>IPrintOemUni::TTDownloadMethod</strong></a></p></td>
<td><p>允许呈现插件指示 Unidrv 应为指定的 TrueType 字体使用的格式。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttygetinfo" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTYGetInfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttygetinfo)"><strong>IPrintOemUni::TTYGetInfo</strong></a></p></td>
<td><p>允许呈现插件提供与纯文本打印机相关的信息 Unidrv。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

