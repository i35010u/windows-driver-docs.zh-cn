---
title: IPrintOemUni COM 接口
description: IPrintOemUni COM 接口
ms.assetid: b120def0-f270-49c6-b12f-10c220801f51
keywords:
- IPrintOemUni
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0ee8a3113ca2e0360a61fe091c08f532f16932
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384214"
---
# <a name="iprintoemuni-com-interface"></a>IPrintOemUni COM 接口





`IPrintOemUni` COM 接口是方式的情况[打印机图形 DLL](printer-graphics-dll.md)为 Unidrv 呈现插件与进行通信。 `IPrintOemUni`接口由每个呈现插件实现。

下表列出并描述所有提供的方法`IPrintOemUni`接口。 呈现插件必须定义所有列出的方法。 如果不需要一种方法，则可以只返回 E\_NOTIMPL。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554216" data-raw-source="[&lt;strong&gt;IPrintOemUni::CommandCallback&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554216)"><strong>IPrintOemUni::CommandCallback</strong></a></p></td>
<td><p>允许呈现插件，以提供动态生成的打印机命令。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554224" data-raw-source="[&lt;strong&gt;IPrintOemUni::Compression&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554224)"><strong>IPrintOemUni::Compression</strong></a></p></td>
<td><p>允许呈现插件，以提供自定义的位图压缩方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554230" data-raw-source="[&lt;strong&gt;IPrintOemUni::DevMode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554230)"><strong>IPrintOemUni::DevMode</strong></a></p></td>
<td><p>对呈现插件的专用 DEVMODE 成员执行操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554232" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554232)"><strong>IPrintOemUni::DisableDriver</strong></a></p></td>
<td><p>释放所分配的呈现插件的资源<strong>IPrintOemUni::EnableDriver</strong>方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554238" data-raw-source="[&lt;strong&gt;IPrintOemUni::DisablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554238)"><strong>IPrintOemUni::DisablePDEV</strong></a></p></td>
<td><p>允许呈现插件，以删除由分配的专用 PDEV 结构及其<a href="https://msdn.microsoft.com/library/windows/hardware/ff554249" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554249)"> <strong>IPrintOemUni::EnablePDEV</strong> </a>方法。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554241" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadCharGlyph&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554241)"><strong>IPrintOemUni::DownloadCharGlyph</strong></a></p></td>
<td><p>允许呈现插件，以指定的软字体的字符标志符号下载到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554242" data-raw-source="[&lt;strong&gt;IPrintOemUni::DownloadFontHeader&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554242)"><strong>IPrintOemUni::DownloadFontHeader</strong></a></p></td>
<td><p>允许呈现插件，以下载到打印机的字体的标头信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554245" data-raw-source="[&lt;strong&gt;IPrintOemUni::DriverDMS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554245)"><strong>IPrintOemUni::DriverDMS</strong></a></p></td>
<td><p>允许呈现插件，以指示它将使用设备管理的绘图图面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554248" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnableDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554248)"><strong>IPrintOemUni::EnableDriver</strong></a></p></td>
<td><p>允许呈现插件出一些图形 DDI 函数挂钩。 请注意，此方法和<strong>IPrintOemUni::DisableDriver</strong>必须考虑作为对; 如果实现了一个，也必须实现其他。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554249" data-raw-source="[&lt;strong&gt;IPrintOemUni::EnablePDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554249)"><strong>IPrintOemUni::EnablePDEV</strong></a></p></td>
<td><p>允许呈现插件，以创建其自己 PDEV 结构。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554252" data-raw-source="[&lt;strong&gt;IPrintOemUni::FilterGraphics&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554252)"><strong>IPrintOemUni::FilterGraphics</strong></a></p></td>
<td><p>允许呈现插件，以修改扫描行数据并将其发送到后台处理程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554253" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetImplementedMethod&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554253)"><strong>IPrintOemUni::GetImplementedMethod</strong></a></p></td>
<td><p>（所需的实现。）允许 Unidrv 确定哪个<code>IPrintOemUni</code>插件呈现的已实现接口方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554256" data-raw-source="[&lt;strong&gt;IPrintOemUni::GetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554256)"><strong>IPrintOemUni::GetInfo</strong></a></p></td>
<td><p>（所需的实现。）返回呈现插件的标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554258" data-raw-source="[&lt;strong&gt;IPrintOemUni::HalftonePattern&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554258)"><strong>IPrintOemUni::HalftonePattern</strong></a></p></td>
<td><p>允许呈现插件，以创建或修改半色调模式，然后在半色调操作中使用。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554261" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554261)"><strong>IPrintOemUni::ImageProcessing</strong></a></p></td>
<td><p>允许呈现插件，以修改图像的位图数据，以便执行颜色格式设置或半色调。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554264" data-raw-source="[&lt;strong&gt;IPrintOemUni::MemoryUsage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554264)"><strong>IPrintOemUni::MemoryUsage</strong></a></p></td>
<td><p>允许呈现插件，以指定通过使用所需的内存量及其<a href="https://msdn.microsoft.com/library/windows/hardware/ff554261" data-raw-source="[&lt;strong&gt;IPrintOemUni::ImageProcessing&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554261)"> <strong>IPrintOemUni::ImageProcessing</strong> </a>方法。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554267" data-raw-source="[&lt;strong&gt;IPrintOemUni::OutputCharStr&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554267)"><strong>IPrintOemUni::OutputCharStr</strong></a></p></td>
<td><p>允许呈现插件，以控制打印的字体标志符号。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554269" data-raw-source="[&lt;strong&gt;IPrintOemUni::PublishDriverInterface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554269)"><strong>IPrintOemUni::PublishDriverInterface</strong></a></p></td>
<td><p>（所需的实现。）提供一个指向 Unidrv 驱动<a href="iprintoemdriveruni-com-interface.md" data-raw-source="[IPrintOemDriverUni COM interface](iprintoemdriveruni-com-interface.md)">IPrintOemDriverUni COM 接口</a>或<a href="https://msdn.microsoft.com/library/windows/hardware/ff552940" data-raw-source="[IPrintCoreHelperUni interface](https://msdn.microsoft.com/library/windows/hardware/ff552940)">IPrintCoreHelperUni 接口</a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554270" data-raw-source="[&lt;strong&gt;IPrintOemUni::ResetPDEV&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554270)"><strong>IPrintOemUni::ResetPDEV</strong></a></p></td>
<td><p>允许呈现插件，以重置其 PDEV 结构。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554274" data-raw-source="[&lt;strong&gt;IPrintOemUni::SendFontCmd&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554274)"><strong>IPrintOemUni::SendFontCmd</strong></a></p></td>
<td><p>允许呈现插件，以修改打印机的字体选择命令，然后将其发送到打印机。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554277" data-raw-source="[&lt;strong&gt;IPrintOemUni::TextOutAsBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554277)"><strong>IPrintOemUni::TextOutAsBitmap</strong></a></p></td>
<td><p>允许呈现插件，以创建位图图像的文本字符串。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554279" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTDownloadMethod&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554279)"><strong>IPrintOemUni::TTDownloadMethod</strong></a></p></td>
<td><p>允许插件，以指示 Unidrv 应使用指定的 TrueType 字体的格式呈现。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554283" data-raw-source="[&lt;strong&gt;IPrintOemUni::TTYGetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554283)"><strong>IPrintOemUni::TTYGetInfo</strong></a></p></td>
<td><p>允许呈现插件 Unidrv 提供与仅限文本的打印机相关的信息。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




