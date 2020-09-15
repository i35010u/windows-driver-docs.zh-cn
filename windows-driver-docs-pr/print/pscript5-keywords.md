---
title: Pscript5 关键字
description: Pscript5 关键字
ms.assetid: a5f4384a-8d78-4dc6-969b-f7a1fa6cb5e7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8fd774f55e7be16049a4aa48cebda6a4e0699978
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107522"
---
# <a name="pscript5-keywords"></a>Pscript5 关键字


从 Pscript5 插件传递到帮助器接口的功能和选项名称是这些功能和选项的字符串名称，如 PPD 文件中所定义的那样。 此外，某些保留字符串是为在 Pscript5 core 驱动程序中实现的功能定义的，这些功能未在 PPD 文件中表示。 请注意，可以通过调用 **EnumOptions**在运行时确定下表中列出的所有选项。 但是，对于需要范围内的数值设置的功能， **EnumOptions**方法将在其*pOptionList*参数中返回**NULL**值，并在 pdwNumOptions 中返回零个选项的计数 \* *pdwNumOptions*。

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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>%AddEuro</p></td>
<td><p></p>
"True"</td>
<td><p>将欧元符号添加到设备字体。</p>
<p>打印机-粘滞。</p>
<p>需要 PostScript 级别2。 请参阅此表后面的注释1。</p></td>
</tr>
<tr class="even">
<td><p>%CtrlDAfter</p></td>
<td><p></p>
"True"</td>
<td><p>每个作业后发送 CTRL + D。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%CtrlDBefore</p></td>
<td><p></p>
"True"</td>
<td><p>在每个作业之前发送 CTRL + D。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>%CustomPageSize</p></td>
<td><p>自定义页面大小选项具有复杂格式。 请参阅此表后面的注释2。</p></td>
<td><p>读取或指定自定义页面大小设置。 设置此功能还会导致公用<a href="/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a>结构的<strong>dmPaperSize</strong>成员重置为 DMPAPER_CUSTOMSIZE (指示 PS 自定义大小) ，并设置 DM_PAPERSIZE 位标志。 此功能只能在公共 DEVMODEW 结构指示正在使用的是自定义纸张大小时才会被读取。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%GraphicsAsTrueGray</p></td>
<td><p></p>
"True"</td>
<td><p>将灰色图形转换为 PostScript 灰色。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>%JobTimeout</p></td>
<td><p>数值 (参阅此表后面的备注 3) </p>
<p>"0" 到 "2147483647"</p></td>
<td><p>指定作业超时（以秒为单位）。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%MaxFontSizeAsBitmap</p></td>
<td><p>数值 (参阅备注 3) </p>
<p>"0" 到 "32767"</p></td>
<td><p>指定作为位图下载的最大字体大小。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>%MetafileSpooling</p></td>
<td><p></p>
"True"</td>
<td><p>启用 EMF 假脱机。 启用此功能相当于启用 <strong>高级打印功能</strong> UI 选项。 请注意，此功能具有与手册打印、排序和页面排序交互的约束。 在针对这些功能中的任何一种进行解析时，此功能具有最低优先级。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%MinFontAsOutline</p></td>
<td><p>数值 (参阅此表后面的备注 3) </p>
<p>"0" 到 "32767"</p></td>
<td><p>指定应下载为大纲的最小字体大小。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>% 镜像</p></td>
<td><p></p>
"True"</td>
<td><p>通过反转水平坐标来镜像输出。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>% 负值</p></td>
<td><p></p>
"True"</td>
<td><p>反转打印页上的黑色和白色区域。</p>
<p>文档-粘滞。</p>
<p>要求使用黑白打印机，而不是彩色。</p></td>
</tr>
<tr class="even">
<td><p>% 方向</p></td>
<td><p></p>
"纵向" "横向" "RotatedLandscape"</td>
<td><p>指定输出方向。 使用此技术配置方向时，将在与<strong>IPrintCoreHelperPS</strong>接口一起使用时，更改 private 和 public <a href="/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a>结构值。 此警告不适用于 <strong>IPrintCoreUI2</strong> 接口。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>% OutputFormat</p></td>
<td><p></p>
"加速" "可移植性" "EPS" "存档"</td>
<td><p>指定 PostScript 输出格式。 输出格式的行为与为 <strong>IPrintCoreUI2</strong>定义的行为相同。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>%OutputProtocol</p></td>
<td><p></p>
"ASCII" "BCP" "TBCP" "Binary"</td>
<td><p>指定打印机将用于打印作业的协议。 BCP 和 TBCP 选项仅在受支持时可用。 <strong>EnumOptions</strong> 仅包括支持的值。 还可以通过检查 "协议" 全局特性来确定输出协议。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%OutputPSLevel</p></td>
<td><p></p>
"1" "2" "3"</td>
<td><p>指定要为此打印作业生成的 PostScript 语言级别。 可用选项限制为等于或小于 "LanguageLevel" 全局特性中指定的设备的语言级别的值。</p>
<p>文档-粘滞。</p>
<p>需要 PostScript Level 2 或更高版本。 请参阅此表后面的注释1。</p></td>
</tr>
<tr class="even">
<td><p>%PageOrder</p></td>
<td><p></p>
"FrontToBack" "BackToFront"</td>
<td><p>指定页面的打印顺序。 如果 EMF 假脱机功能不可用，则在调用 <strong>EnumFeatures</strong>时不会列出此功能，尝试读取或写入此功能的设置将返回 E_FAIL。 Additionaly，如果% MetafileSpooling 功能设置为 False，则 BackToFront 将受到限制。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%PagePerSheet</p></td>
<td><p></p>
"1"、"2"、"4"、"6"、"9"、"16"、"手册"</td>
<td><p>仅当双面显示可用时，才能使用手册打印功能。 如果未打开，则设置 "手册" 选项将导致启用双面打印。 如果关闭了双面并选择了 "手册打印"，则该选项将被强制设置为 "2"。 如果禁用了图元文件假脱机，则会将其表示为手册打印的约束。 如果 EMF 假脱机因为正在使用打印处理器而不可用，则手册打印将不可用。 在这种情况下，将不会在 <strong>EnumOptions</strong>中列出手册打印，如果调用方请求 "% PagePerSheet" 设置为 "手册"，则 <strong>SetOptions</strong> 将返回 E_FAIL。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>%PSErrorHandler</p></td>
<td><p></p>
"True"</td>
<td><p>发送 PostScript 错误处理程序。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%PSMemory</p></td>
<td><p>数值 (参阅此表后面的备注 3) </p>
<p>对于 PostScript 级别1打印机，范围为 "172" 到 "2097151"。</p>
<p>对于 Postscript 级别2或3打印机，范围为 "249" 到 "2097151"。</p></td>
<td><p>指定设备上可用的虚拟内存的 kb 数。 请注意，值以 kb 表示，而不是以字节为单位。 另请注意，对于级别1和级别2打印机，有效范围有所不同。 尝试设置这些范围以外的值将失败，并 E_FAIL 为 HRESULT。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>%TextTrueGray</p></td>
<td><p></p>
"True"</td>
<td><p>将灰色文本转换为 PostScript 灰色。</p>
<p>打印机-粘滞。</p></td>
</tr>
<tr class="odd">
<td><p>%TTDownloadFormat</p></td>
<td><p></p>
"自动" 大纲 "" Bitmap "" NativeTrueType "</td>
<td><p>指定 TrueType 字体下载格式。 仅当 "TTRasterizer" 全局特性指示对 "Type42" 的支持时，NativeTrueType 才可用且列在 <strong>EnumOptions</strong> 中。</p>
<p>文档-粘滞。</p></td>
</tr>
<tr class="even">
<td><p>% WaitTimeout</p></td>
<td><p>数值 (参阅此表后面的备注 3) </p>
<p>"0" 到 "2147483647"</p></td>
<td><p>指定等待超时值（以秒为单位）。</p>
<p>打印机-粘滞。</p></td>
</tr>
</tbody>
</table>

 

**注意**   1如果某个功能未满足规定的要求，则该功能将不会在**EnumFeatures**中列出，尝试获取或设置该功能将导致无法返回 E \_ 。 本说明适用于% AddEuro、% 负值和% OutputPSLevel。

 

**注意**   2 (% CustomPageSize) 自定义页面大小格式与**IPrintCoreUI2**中所述的格式相同。 **EnumOptions** 返回空的选项列表。

 

**注意**   3个数值表示为只包含数字字符的 ANSI 字符串。 不允许使用符号符号。 例如，"300" 有效，但 "-20"、"20.5" 和 "+ 300" 均无效。 本说明适用于% JobTimeout、% MaxFontSizeAsBitmap、% MinFontAsOutline、% PSMemory 和% WaitTimeout。

 

