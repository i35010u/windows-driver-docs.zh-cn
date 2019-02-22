---
title: Pscript5 关键字
description: Pscript5 关键字
ms.assetid: a5f4384a-8d78-4dc6-969b-f7a1fa6cb5e7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdeff8de3790a63d3ad4f9621c19cf78580763a9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547971"
---
# <a name="pscript5-keywords"></a>Pscript5 关键字


功能和选项传递给帮助程序接口从 Pscript5 插件的名称为 PPD 文件中定义的功能和选项的字符串名称。 此外，某些保留的字符串定义在 Pscript5 核心驱动程序中实现不会出现在 PPD 文件的功能。 请注意，所有以下表中列出的选项可以确定在运行时通过调用**EnumOptions**。 但是，对于需要数字设置范围中的功能**EnumOptions**方法将返回**NULL**中的值及其*pOptionList*参数和计数为零中的选项\* *pdwNumOptions*。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能名称</th>
<th>选项</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>%AddEuro</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>将欧元符号添加到设备字体。</p>
<p>打印机粘性。</p>
<p>需要 PostScript 级别 2。 请参阅备注 1 此表后面。</p></td>
</tr>
<tr class="even">
<td><p>%CtrlDAfter</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>每个作业之后发送 CTRL + D。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%CtrlDBefore</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>每个作业之前发送 CTRL + D。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="even">
<td><p>%CustomPageSize</p></td>
<td><p>自定义页面大小选项具有复杂的格式。 请参阅备注 2 此表后面。</p></td>
<td><p>读取或指定自定义页面大小设置。 设置此功能还会导致<strong>dmPaperSize</strong>的公共成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>结构，以重置为 DMPAPER_CUSTOMSIZE （指示 PS 自定义大小） 和集DM_PAPERSIZE 位标志。 此功能可以是只读的公共 DEVMODEW 结构是否指示自定义纸张大小正在使用。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%GraphicsAsTrueGray</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>将纯灰度图形转换为 PostScript 灰色。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="even">
<td><p>%JobTimeout</p></td>
<td><p>数值 （请参阅备注 3 此表后面）</p>
<p>&quot;0&quot;通过&quot;2147483647&quot;</p></td>
<td><p>以秒为单位指定作业超时。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%MaxFontSizeAsBitmap</p></td>
<td><p>数值 （请参阅备注 3）</p>
<p>&quot;0&quot;通过&quot;32767&quot;</p></td>
<td><p>指定要作为位图下载的最大字体大小。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="even">
<td><p>%MetafileSpooling</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>启用 EMF 后台处理。 启用此功能是等效于启用<strong>高级打印功能</strong>UI 选项。 请注意，此功能与手册打印、 排序规则，和页面顺序进行交互的约束。 解析对任何这些功能时，此功能是提供最低的优先级。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%MinFontAsOutline</p></td>
<td><p>数值 （请参阅备注 3 此表后面）</p>
<p>&quot;0&quot;通过&quot;32,767&quot;</p></td>
<td><p>指定应下载的最小字体大小为大纲。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="even">
<td><p>%Mirroring</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>镜像输出通过反转的水平坐标。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%Negative</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>反向打印黑色或白色区域。</p>
<p>文档粘性。</p>
<p>需要黑白打印机、 不颜色。</p></td>
</tr>
<tr class="even">
<td><p>%Orientation</p></td>
<td><p></p>
&quot;Portrait&quot; &quot;Landscape&quot; &quot;RotatedLandscape&quot;</td>
<td><p>指定输出方向。 使用此技术配置方向更改私有和公共<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>结构的值，与一起使用时<strong>IPrintCoreHelperPS</strong>接口。 此警告不适用于<strong>IPrintCoreUI2</strong>接口。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%OutputFormat</p></td>
<td><p></p>
&quot;速度&quot;&quot;可移植性&quot; &quot;EPS&quot; &quot;存档&quot;</td>
<td><p>指定 PostScript 输出格式。 输出格式的行为是为定义的相同<strong>IPrintCoreUI2</strong>。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="even">
<td><p>%OutputProtocol</p></td>
<td><p></p>
&quot;ASCII&quot; &quot;BCP&quot; &quot;TBCP&quot; &quot;Binary&quot;</td>
<td><p>指定将使用打印机来打印作业的协议。 仅当受可用的 BCP 和 TBCP 选项。 <strong>EnumOptions</strong>包括支持的值。 此外可以通过检查来确定输出协议&quot;协议&quot;的全局属性。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%OutputPSLevel</p></td>
<td><p></p>
&quot;1&quot; &quot;2&quot; &quot;3&quot;</td>
<td><p>指定要为此打印作业生成的 PostScript 语言级别。 可用的选项仅限于值等于或小于中指定的语言级别的设备&quot;LanguageLevel&quot;的全局属性。</p>
<p>文档粘性。</p>
<p>需要 PostScript 级别 2 或更高版本。 请参阅备注 1 此表后面。</p></td>
</tr>
<tr class="even">
<td><p>%PageOrder</p></td>
<td><p></p>
&quot;FrontToBack&quot; &quot;BackToFront&quot;</td>
<td><p>指定要打印的页面的顺序。 如果 EMF 后台处理不可用，调用时将不会列出此功能<strong>EnumFeatures</strong>，并尝试读取或写入设置，此功能将返回 E_FAIL。 另外，BackToFront 将受到限制，如果 %metafilespooling 功能设置为 False。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%PagePerSheet</p></td>
<td><p></p>
&quot;1&quot;， &quot;2&quot;， &quot;4&quot;， &quot;6&quot;， &quot;9&quot;， &quot;16&quot;，&quot;手册&quot;</td>
<td><p>打印手册是双工是可用时才可用。 设置&quot;手册&quot;选项将导致进行双面打印，如果已不在开启。 如果双工模式处于关闭状态，并选择手册打印，将 2 向上到强制选项。 如果禁用元文件后台打印，则它将表示为手册打印的约束。 如果 EMF 后台处理不可用，因为正在使用的打印处理器，手册打印将不可用。 在这种情况下，将不会打印手册列出在<strong>EnumOptions</strong>，并<strong>SetOptions</strong>将返回 E_FAIL，如果调用方请求&quot;%pagepersheet&quot;设置为&quot;手册&quot;。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="even">
<td><p>%PSErrorHandler</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>发送 PostScript 错误处理程序。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%PSMemory</p></td>
<td><p>数值 （请参阅备注 3 此表后面）</p>
<p>对于 PostScript 级别 1 打印机，范围是&quot;172&quot;通过&quot;2097151&quot;。</p>
<p>对于 Postscript 级别 2 或 3 的打印机，范围是&quot;249&quot;通过&quot;2097151&quot;。</p></td>
<td><p>指定可在设备的虚拟内存的千字节数。 请注意值都以千字节为单位，并不是字节表示。 另请注意，有效范围不同于级别 1 和 2 级打印机。 尝试设置这些范围之外的值将因 E_FAIL HRESULT。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="even">
<td><p>%TextTrueGray</p></td>
<td><p></p>
&quot;True&quot; &quot;False&quot;</td>
<td><p>灰色文本转换为 PostScript 灰色。</p>
<p>打印机粘性。</p></td>
</tr>
<tr class="odd">
<td><p>%TTDownloadFormat</p></td>
<td><p></p>
&quot;Automatic&quot; &quot;Outline&quot; &quot;Bitmap&quot; &quot;NativeTrueType&quot;</td>
<td><p>指定 TrueType 字体下载格式。 NativeTrueType 是可用在中并列出<strong>EnumOptions</strong>仅当&quot;TTRasterizer&quot;全局属性指示支持&quot;Type42&quot;。</p>
<p>文档粘性。</p></td>
</tr>
<tr class="even">
<td><p>%WaitTimeout</p></td>
<td><p>数值 （请参阅备注 3 此表后面）</p>
<p>&quot;0&quot;通过&quot;2147483647&quot;</p></td>
<td><p>以秒为单位指定等待超时值。</p>
<p>打印机粘性。</p></td>
</tr>
</tbody>
</table>

 

**请注意**   1 的一项功能不满足规定的要求时，该功能将不会列出在**EnumFeatures**，并尝试获取或设置该功能将导致电子\_无法返回。 本说明适用于 %addeuro、 负数 %和 %outputpslevel。

 

**请注意**   2 （%custompagesize) 自定义页面大小格式等同于中所述**IPrintCoreUI2**。 **EnumOptions**返回空列表的选项。

 

**请注意**   3 个数字值表示为仅包含数字字符的 ANSI 字符串。 不允许登录的符号。 例如，"300"是有效的但是"-20"、"20.5"和"+ 300"都无效。 本说明适用于 %jobtimeout、 %MaxFontSizeAsBitmap、 %minfontasoutline、 PSMemory，%和 %waittimeout。

 

 

 




