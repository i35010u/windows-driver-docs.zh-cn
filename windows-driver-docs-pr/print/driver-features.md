---
title: 驱动程序功能
description: 驱动程序功能
ms.assetid: 56efebda-970f-4885-9c5f-1eac97aecfdd
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 55104c73a6d77947298d69ea78d649495b96fcf1
ms.sourcegitcommit: 17c1bbc5ea0bef3bbc87794b030a073f905dc942
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802411"
---
# <a name="driver-features"></a>驱动程序功能

驱动程序功能是由驱动程序合成的非 PPD 功能 (例如， **% OutputFormat** 功能) 。 若要避免与 PPD 功能关键字名称冲突，所有驱动程序功能关键字名称前面都有一个 "%" 字符。 驱动程序功能/选项关键字也区分大小写。

若要获取驱动程序支持的所有驱动程序功能关键字的列表，插件可以调用 EnumFeatures，这将返回包含驱动程序功能和 PPD 功能的功能关键字列表。 然后，该插件可以搜索以 "%" 前缀开头的功能关键字名称以获取驱动程序功能列表。

下表列出了当前支持的驱动程序功能。 表中的每一行都列出了驱动程序功能关键字，其中显示了支持的选项，说明是否可以在对 EnumOptions 的调用中枚举功能的选项，并提供简短说明。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>驱动程序功能</th>
<th>支持的选项</th>
<th>枚举选项？</th>
<th>描述和注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>%AddEuro</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>将欧元符号添加到设备字体。</p>
<p>只有2级 + 打印机支持此功能。 对于第1级打印机， <strong>SetOptions</strong> 将忽略此功能， <strong>GetOptions</strong> 始终返回 "False"。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%CtrlDAfter</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>在每个作业之后发送 Ctrl-c。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%CtrlDBefore</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>在每个作业之前发送 Ctrl + D。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%CustomPageSize</strong></p></td>
<td><p>有关详细信息，请参阅下面的注释1。</p></td>
<td><p>否</p></td>
<td><p>指定 PostScript 自定义页面大小参数。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%GraphicsTrueGray</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>将灰色图形转换为 PostScript 灰色。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%JobTimeout</strong></p></td>
<td><p>一个以 NULL 结尾的 ANSI 字符串，其中包含表示超时的无符号整数（范围为0到2147483647）。</p>
<p>对于 <strong>SetOptions</strong>，允许使用十进制数字前后的额外制表符或空格字符，但不允许使用符号符号。</p></td>
<td><p>否</p></td>
<td><p>指定作业超时值。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%MaxFontSizeAsBitmap</strong></p></td>
<td><p>一个以 NULL 结尾的 ANSI 字符串，其中包含表示0到32767范围内的无符号整数值的十进制数字字符。</p>
<p>对于 <strong>SetOptions</strong>，允许使用十进制数字前后的额外制表符或空格字符，但不允许使用符号符号。</p></td>
<td><p>否</p></td>
<td><p>指定作为位图下载的最大字体大小。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%MetafileSpooling</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>启用/禁用高级打印功能。</p>
<p>文档-粘滞</p>
<p>有关详细信息，请参阅下面的注释2。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%MinFontSizeAsOutline</strong></p></td>
<td><p>一个以 NULL 结尾的 ANSI 字符串，其中包含表示0到32767范围内的无符号整数值的十进制数字字符。</p>
<p>对于 <strong>SetOptions</strong>，允许使用十进制数字前后的额外制表符或空格字符，但不允许使用符号符号。</p></td>
<td><p>否</p></td>
<td><p>指定要下载为大纲的最小字体大小。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>% 镜像</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>通过反转水平坐标来镜像输出。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>% 负值</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>通过反转黑色和白色的值生成负片输出。 只有黑色和白色打印机支持此功能。 对于彩色打印机， <strong>SetOptions</strong> 将忽略此功能， <strong>GetOptions</strong> 始终返回 "False"。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>% 方向</strong></p></td>
<td><p>"纵向"、"横向"、"RotatedLandscape"</p></td>
<td><p>是</p></td>
<td><p>指定输出方向。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>% OutputFormat</strong></p></td>
<td><p>"速度"、"可移植性"、"EPS"、"存档"</p></td>
<td><p>是</p></td>
<td><p>指定 PostScript 输出格式。</p>
<p>文档-粘滞</p>
<p>有关详细信息，请参阅下面的注释5。</p></td>
</tr>
<tr class="even">
<td><p><strong>%OutputProtocol</strong></p></td>
<td><p>"ASCII"、"BCP"、"TBCP" 和 "Binary"</p></td>
<td><p>是</p></td>
<td><p>指定打印机将用于打印作业的协议。 假设 PostScript 打印机支持 "ASCII" 和 "二进制"，因此这些选项始终可用。 "BCP" 和 "TBCP" 选项仅在受支持时可用。  (要找出这种情况，请检查全局特性 "协议"。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%OutputPSLevel</strong></p></td>
<td><p>"1"、"2"、"3"</p></td>
<td><p>否</p></td>
<td><p>指定打印作业要使用的 PostScript 语言级别。 此设置永远不会大于 "LanguageLevel" 全局特性中指定的值。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%PageOrder</strong></p></td>
<td><p>"FrontToBack"</p>
<p>"BackToFront"</p></td>
<td><p>是</p></td>
<td><p>指定打印页面的顺序。</p>
<p>文档-粘滞</p>
<p>有关详细信息，请参阅下面的注释3。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PagePerSheet</strong></p></td>
<td><p>"1"、"2"、"4"、"6"、</p>
<p>"9"、"16"、"手册"</p></td>
<td><p>是</p></td>
<td><p>指定每个物理表的逻辑页数。 此功能也称为 "N 向上" 打印。</p>
<p>文档-粘滞</p>
<p>有关详细信息，请参阅下面的备注4。</p></td>
</tr>
<tr class="even">
<td><p><strong>%PSErrorHandler</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>发送 PostScript 错误处理程序。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PSMemory</strong></p></td>
<td><p>一个以 NULL 结尾的 ANSI 字符串，其中包含表示 PostScript 内存的无符号整数（范围为0到2147483647）的十进制数字字符。</p>
<p>对于 <strong>SetOptions</strong>，允许使用十进制数字前后的额外制表符或空格字符，但不允许使用符号符号。</p></td>
<td><p>否</p></td>
<td><p>指定可用的 PostScript 虚拟内存量。</p>
<p>核心驱动程序需要一定数量的可用 PostScript 虚拟内存来进行处理。 如果在此最小值下面设置 <strong>% PSMemory</strong> ，则最小值将用作新值。 目前，1级打印机的最小值为 172 KB，2级打印机的最小值为 249 KB。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%TextTrueGray</strong></p></td>
<td><p>“True”</p>
<p>“False”</p></td>
<td><p>是</p></td>
<td><p>将灰色文本转换为 PostScript 灰色。</p>
<p>打印机-粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%TTDownloadFormat</strong></p></td>
<td><p>"Automatic"、"大纲"、"Bitmap"、"NativeTrueType"</p></td>
<td><p>是</p></td>
<td><p>指定 TrueType 字体下载格式。 仅当 "TTRasterizer" 全局特性指示对 "Type42" 的支持时，才支持 "NativeTrueType"。</p>
<p>文档-粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>% WaitTimeout</strong></p></td>
<td><p>一个以 NULL 结尾的 ANSI 字符串，其中包含表示超时的无符号整数（范围为0到2147483647）。</p>
<p>对于 <strong>SetOptions</strong>，允许使用十进制数字前后的额外制表符或空格字符，但不允许使用符号符号。</p></td>
<td><p>否</p></td>
<td><p>指定等待超时值。</p>
<p>打印机-粘滞</p></td>
</tr>
</tbody>
</table>

## <a name="notes-on-driver-feature-keywords"></a>驱动程序功能关键字说明

1. **% CustomPageSize**驱动程序功能具有五个选项值： x、y、WidthOffset、HeightOffset 和 FeedDirection。 有关这些参数的详细说明，请参阅 *PostScript 打印机说明文件格式规范*的第5.16 节，版本4.3。

    **% CustomPageSize**项包含 **% CustomPageSize**关键字，以及 x、y、WidthOffset、HeightOffset 和 FeedDirection 选项的值。 第一项是% CustomPageSize 关键字，后面跟 NULL 字符。 X、y、WidthOffset 和 HeightOffset 的值遵循此关键字，并显示为无符号十进制数字的子字符串，每个字符串表示相应选项值的 PostScript 点数。 其中每个数值后跟一个或多个空格或制表符。 字符串中的最后一项是 FeedDirection 的值，该值由 NULL 字符终止。 FeedDirection 的选项是 "LongEdge"、"ShortEdge" (对应于 "方向 0" 和 "1) "，"LongEdgeFlip"，"ShortEdgeFlip" (对应于 "方向 2" 和 "3") 。 检查** \* LeadingEdge** PPD 功能关键字以获取支持的源方向。

    对于 **GetOptions**， *pmszFeatureOptionBuf* 指向的输出缓冲区如上一段中所述。 在下面的示例中，x 的值为612，y 的值为792，WidthOffset 和 HeightOffset 的值均为0，FeedDirection 的值为 "ShortEdge"。

    ```cpp
    "%CustomPageSize\0612 792 0 0 ShortEdge\0"
    ```

    对于 **SetOptions**，允许使用十进制数字前后的额外制表符或空格字符，但不允许使用符号符号。 否则，应按如上所述构造 *pmszFeatureOptionBuf* 所指向的输入缓冲区。

2. 仅当满足以下所有三个条件时，才支持 **% CustomPageSize** 驱动程序功能：
    1. PPD 文件包含** \* CustomPageSize**功能。
    2. ** \* PPD-Adobe**关键字的值大于或等于4.3，或指定** \* UseHWMargin**： **False**来指示滚动更新的设备。
    3. ** \* PageSize** PPD 功能的当前选定选项为 CustomPageSize。

3. 仅当启用了后台处理程序 EMF 假脱机功能时，才支持此功能。

    如果支持此功能，则将此功能的选项设置为 "False" 将导致对以下 EMF 相关功能的更改：

    1. 如果 **% PagePerSheet** 是 "手册"，则将其更改为 "1"。
    2. 如果 "逐份打印" 设置为 "True" (可以直接在[**DEVMODEW**](https://docs.microsoft.com/windows/win32/api/wingdi/ns-wingdi-devmodew)结构的公共部分中设置，也可以通过在 " ** \* 逐份打印**") 功能上调用**SetOptions**来设置，但排序功能当前不可用，则 collate 将设置为 "False"。
    3. 如果 **% PageOrder** 与打印机的当前输出顺序设置相反，则 **% PageOrder** 将反转到打印机的值。

4. 仅当启用了后台处理程序 EMF 假脱机功能时，才支持此功能。

    如果支持此功能，则设置此功能可能会导致以下情况发生：

    1. 如果打印机的 PPD 文件包含** \* OutputOrder**功能关键字，则会更改其选项选择，以匹配 **% PageOrder**功能的新设置的输出顺序。 这样做是为了防止后台处理程序执行不必要的页面顺序模拟。
    2. 如果打印机的 PPD 文件不包括** \* OutputOrder**功能，并且 **% PageOrder**驱动程序功能的新设置与打印机的当前输出顺序设置相反，而 **% MetafileSpooling**驱动程序功能为 "False"，则 **% MetafileSpooling**将重置为 "True"。

5. 仅当启用了后台处理程序 EMF 假脱机且双工功能可用时，才支持 "手册" 选项。

    支持 "手册" 选项时，将 **% PagePerSheet** driver 功能设置为 "手册" 可能会导致以下更改：

    1. 如果 **% MetafileSpooling** driver 功能为 "False"，则会将其重置为 "True"。
    2. 如果** \* 双工**PPD 功能设置为 "无"， ** \* 双工**功能将重置为 PPD 文件中定义的第一个非单工选项。

6. 除了 "EPS" (封装的 PostScript) ，根据以下两个特征分类了 **% OutputFormat** driver 功能中指定的格式：
    1. 输出 PostScript 代码是否独立于页面顺序？
    2. 输出 PostScript 代码是否包含设备控制命令， (通常使用 **setpagedevice** 运算符) ？

        <table>
        <colgroup>
        <col width="33%" />
        <col width="33%" />
        <col width="33%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th></th>
        <th>独立于页面顺序</th>
        <th>setpagedevice</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td><p>Archive</p></td>
        <td><p>是</p></td>
        <td><p>否</p></td>
        </tr>
        <tr class="even">
        <td><p>可移植性</p></td>
        <td><p>是</p></td>
        <td><p>是</p></td>
        </tr>
        <tr class="odd">
        <td><p>Speed</p></td>
        <td><p>否</p></td>
        <td><p>是</p></td>
        </tr>
        </tbody>
        </table>

当在驱动程序功能关键字上调用 **GetOptions** 时，如果未识别请求的特征关键字，或在当前 *文档-粘滞* 或 *打印机粘滞* 模式下识别但不支持此特征关键字 (参阅) [替换驱动程序提供的属性表页](replacing-driver-supplied-property-sheet-pages.md) ，则该功能将被忽略，并且输出缓冲区将不包含其功能/选项关键字对。

例如，假设调用了 **GetOptions** 方法， *pmszFeaturesRequested* 输入缓冲区包含以下 (以多个 \_ SZ 格式) 的字符串：

```cpp
"Resolution\0%CustomPageSize\0Unknown_Name\0%Orientation\0\0"
```

在 **GetOption** 返回后， *pmszFeatureOptionBuf* 输出缓冲区可能包含此字符串 (以多个 \_ SZ 格式) ：

```cpp
"Resolution\0300dpi\0%CustomPageSize\0612 792 0 0 ShortEdge\0%Orientation\0RotatedLandscape\0\0"
```

请注意， \_ 第一个字符串中不) 存在的 "未知名称" 功能 (不会出现在第一个字符串中，因为它不是由 Pscript 驱动程序识别的。 其他功能（分辨率、 **百分比 CustomPageSize**和 **% 方向**）连同其当前选项一起出现在输出字符串中，分别是 "300dpi"、"612 792 0 0 ShortEdge" 和 "RotatedLandscape"。 有关 **% CustomPageSize** 选项的说明，请参阅驱动程序功能。

当在驱动程序功能关键字上调用 **SetOptions** 时，如果未识别所请求的功能关键字或在 *pmszFeatureOptionBuf* 指向的输入缓冲区中的 option 关键字，或者该功能已被识别但在当前文档中或打印机粘滞模式下不受支持 (参阅) 中 [替换驱动程序提供的属性表页](replacing-driver-supplied-property-sheet-pages.md) 。要么识别了 feature 关键字及其 option 关键字，但选项关键字对于该功能无效 (例如，尝试在不支持 Type42 TTRasterizer) 的打印机上将 **% TTDownloadFormat** 设置为 "NativeTrueType"，则将忽略该功能/选项对，该功能的当前选项将继续生效。

*PmszFeatureOptionBuf*所指向的缓冲区中的功能/选项关键字对的顺序可能会影响**SetOptions**调用的结果。 例如，下面两个不同的订单具有不同的结果。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th><em>pmszFeatureOptionBuf</em></th>
<th>%PagePerSheet</th>
<th>%MetafileSpooling</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"%MetafileSpooling\0False\0%PagePerSheet\0Booklet\0\0"</p></td>
<td><p>单</p></td>
<td><p>“True”</p></td>
</tr>
<tr class="even">
<td><p>"%PagePerSheet\0Booklet\0%MetafileSpooling\0False\0\0"</p></td>
<td><p>"1"</p></td>
<td><p>“False”</p></td>
</tr>
</tbody>
</table>

有关这些结果的出现原因的说明，请参阅上面的注释 3 **% MetafileSpooling**。
