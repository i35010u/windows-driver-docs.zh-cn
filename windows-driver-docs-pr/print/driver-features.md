---
title: 驱动程序功能
description: 驱动程序功能
ms.assetid: 56efebda-970f-4885-9c5f-1eac97aecfdd
ms.date: 01/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: 48eec98b29f660b525cb4e46a0836219dc18d882
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356084"
---
# <a name="driver-features"></a>驱动程序功能

驱动程序功能是通过该驱动程序合成的非 PPD 功能 (例如， **%outputformat**功能)。 若要避免与 PPD 功能关键字名称冲突，所有驱动程序功能关键字名称的前面"%"字符。 驱动程序功能/选项关键字也是区分大小写的。

若要获取的所有驱动程序列表的驱动程序支持的功能关键字，插件可以调用 EnumFeatures，将返回包含驱动程序功能和 PPD 功能的功能关键字列表。 该插件可以然后搜索功能关键字的名称以"%"前缀来获取驱动程序功能列表开头。

下表列出了当前支持的驱动程序功能。 表中的每一行列出驱动程序功能关键字、 显示受支持的选项、 状态是否可以在调用 EnumOptions，枚举功能的选项并提供简要说明。

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
<th>说明和注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>%AddEuro</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>将欧元符号添加到设备字体。</p>
<p>此功能仅支持级别 2 + 打印机。 级别 1 打印机<strong>SetOptions</strong>会忽略此功能，并<strong>GetOptions</strong>始终返回"False"。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%CtrlDAfter</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>每个作业之后发送 CTRL-D。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%CtrlDBefore</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>每个作业之前发送 CTRL-D。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%CustomPageSize</strong></p></td>
<td><p>有关详细信息，请参阅下面的备注 1。</p></td>
<td><p>否</p></td>
<td><p>指定 PostScript 自定义页面大小参数。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%GraphicsTrueGray</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>将纯灰度图形转换为 PostScript 灰色。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%JobTimeout</strong></p></td>
<td><p>以 NULL 结尾的 ANSI 字符串包含表示无符号的整数来表示超时值，范围为 0 到 2,147,483,647 之间的秒数的十进制数字字符。</p>
<p>有关<strong>SetOptions</strong>、 额外选项卡上或空格字符之前或之后允许的十进制数字，但不是允许正负符号。</p></td>
<td><p>否</p></td>
<td><p>指定作业超时值。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%MaxFontSizeAsBitmap</strong></p></td>
<td><p>以 NULL 结尾的 ANSI 字符串包含表示无符号的整数中的像素数，范围 0 到 32767 之间的十进制数字字符。</p>
<p>有关<strong>SetOptions</strong>、 额外选项卡上或空格字符之前或之后允许的十进制数字，但不是允许正负符号。</p></td>
<td><p>否</p></td>
<td><p>指定要作为位图下载的最大字体大小。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%MetafileSpooling</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>启用/禁用高级打印功能。</p>
<p>文档粘滞</p>
<p>有关详细信息，请参阅下面的备注 2。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%MinFontSizeAsOutline</strong></p></td>
<td><p>以 NULL 结尾的 ANSI 字符串包含表示无符号的整数中的像素数，范围 0 到 32767 之间的十进制数字字符。</p>
<p>有关<strong>SetOptions</strong>、 额外选项卡上或空格字符之前或之后允许的十进制数字，但不是允许正负符号。</p></td>
<td><p>否</p></td>
<td><p>指定要当作轮廓下载的最小字体大小。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%Mirroring</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>镜像输出通过反转的水平坐标。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%Negative</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>通过反转的黑色和白色值生成负数的输出。 此功能仅支持黑白打印机。 对彩色打印机<strong>SetOptions</strong>会忽略此功能，并<strong>GetOptions</strong>始终返回"False"。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%Orientation</strong></p></td>
<td><p>"Portrait", "Landscape", "RotatedLandscape"</p></td>
<td><p>是</p></td>
<td><p>指定输出方向。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%OutputFormat</strong></p></td>
<td><p>"速度"、"可移植性"、"EPS"，"存档"</p></td>
<td><p>是</p></td>
<td><p>指定 PostScript 输出格式。</p>
<p>文档粘滞</p>
<p>有关详细信息，请参阅下面的备注 5。</p></td>
</tr>
<tr class="even">
<td><p><strong>%OutputProtocol</strong></p></td>
<td><p>"ASCII", "BCP", "TBCP", "Binary"</p></td>
<td><p>是</p></td>
<td><p>指定打印机的打印作业将使用的协议。 假定 postScript 打印机都支持"ASCII"和"Binary"，因此将始终显示这些选项。 "BCP"和"TBCP"选项是支持它们时才可用。 （若要查找此输出，请检查全局属性"协议"。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%OutputPSLevel</strong></p></td>
<td><p>"1", "2", "3"</p></td>
<td><p>否</p></td>
<td><p>指定要用于打印作业的 PostScript 语言级别。 该设置将不会大于"LanguageLevel"全局属性中指定的值。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%PageOrder</strong></p></td>
<td><p>"FrontToBack"</p>
<p>"BackToFront"</p></td>
<td><p>是</p></td>
<td><p>指定打印页的顺序。</p>
<p>文档粘滞</p>
<p>有关详细信息，请参阅下面的备注 3。</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PagePerSheet</strong></p></td>
<td><p>"1", "2", "4", "6",</p>
<p>"9"、"16"，"手册"</p></td>
<td><p>是</p></td>
<td><p>指定的每个物理表的逻辑页数。 此功能也称为"每张"打印。</p>
<p>文档粘滞</p>
<p>有关详细信息，请参阅下面的注意 4。</p></td>
</tr>
<tr class="even">
<td><p><strong>%PSErrorHandler</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>发送 PostScript 错误处理程序。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%PSMemory</strong></p></td>
<td><p>以 NULL 结尾的 ANSI 字符串包含表示无符号的整数的 PostScript 内存，在 0 到 2,147,483,647 之间的范围中的千字节数的十进制数字字符。</p>
<p>有关<strong>SetOptions</strong>、 额外选项卡上或空格字符之前或之后允许的十进制数字，但不是允许正负符号。</p></td>
<td><p>否</p></td>
<td><p>指定可用 PostScript 虚拟内存量。</p>
<p>核心驱动程序为其处理需要一定量的可用 PostScript 虚拟内存。 如果<strong>%psmemory</strong>设置低于此最小值、 最小值将用作新值。 目前的最小值是 1 级打印机的 172 KB 和级别 2 + 打印机 249 KB。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%TextTrueGray</strong></p></td>
<td><p>"True"</p>
<p>"False"</p></td>
<td><p>是</p></td>
<td><p>灰色文本转换为 PostScript 灰色。</p>
<p>打印机粘滞</p></td>
</tr>
<tr class="odd">
<td><p><strong>%TTDownloadFormat</strong></p></td>
<td><p>"Automatic", "Outline", "Bitmap", "NativeTrueType"</p></td>
<td><p>是</p></td>
<td><p>指定 TrueType 字体下载格式。 仅当"TTRasterizer"全局属性指示对"Type42"的支持时，才支持"NativeTrueType"。</p>
<p>文档粘滞</p></td>
</tr>
<tr class="even">
<td><p><strong>%WaitTimeout</strong></p></td>
<td><p>以 NULL 结尾的 ANSI 字符串包含表示无符号的整数来表示超时值，范围为 0 到 2,147,483,647 之间的秒数的十进制数字字符。</p>
<p>有关<strong>SetOptions</strong>、 额外选项卡上或空格字符之前或之后允许的十进制数字，但不是允许正负符号。</p></td>
<td><p>否</p></td>
<td><p>指定等待超时值。</p>
<p>打印机粘滞</p></td>
</tr>
</tbody>
</table>

## <a name="notes-on-driver-feature-keywords"></a>有关驱动程序功能关键字的说明

1. **%Custompagesize**驱动程序功能具有五个选项值： x、 y、 WidthOffset、 HeightOffset 和 FeedDirection。 请参阅的部分 5.16 *PostScript 打印机说明文件格式规范、 版本 4.3*，这些参数的详细说明。

    一个 **%custompagesize**条目包含 **%custompagesize**关键字，以及用于 x、 y、 WidthOffset、 HeightOffset 和 FeedDirection 选项的值。 第一项是 %custompagesize 关键字后, 跟 NULL 字符。 X 的值，y，WidthOffset 和 HeightOffset 紧跟此关键字，并显示为无符号的十进制数字的子字符串，是每个资源表示 PostScript 数为相应的选项值点。 每个这些数字的值后跟一个或多个空格或制表符字符。 在字符串中的最后一个项目是 FeedDirection，终止 NULL 字符的值。 FeedDirection 的选项是"LongEdge"、"ShortEdge"（对应于 0 和 1 的方向），和"LongEdgeFlip"、"ShortEdgeFlip"（对应于方向 2 和 3）。 检查 **\*LeadingEdge** PPD 功能关键字来指定受支持的源方向。

    有关**GetOptions**，指向输出缓冲区*pmszFeatureOptionBuf*是上一段中所述。 在以下示例中，x 的值是 612、 y 的值是 792、 WidthOffset 和 HeightOffset 的值均为这两个 0 和 FeedDirection 的值是"ShortEdge"。

    ```cpp
    "%CustomPageSize\0612 792 0 0 ShortEdge\0"
    ```

    有关**SetOptions**、 额外选项卡上或空格字符之前或之后允许的十进制数字，但不是允许正负符号。 否则，输入的缓冲区指向通过*pmszFeatureOptionBuf*应构造，如上文所述。

2. **%Custompagesize**仅当满足以下条件的所有三个支持驱动程序功能：
    1. PPD 文件包含 **\*CustomPageSize**功能。
    2. **\*PPD Adobe**关键字的值大于或等于 4.3，或 **\*UseHWMargin**:**False**指定指示在滚动送纸的设备。
    3. **\*PageSize** PPD 功能当前所选的选项是 CustomPageSize。

3. 仅当已启用后台处理程序 EMF 后台处理时，才支持此功能。

    支持时，此功能的选项设置为"False"可导致更改的 EMF 相关的以下功能：

    1. 如果 **%pagepersheet**是"手册"，它将更改为"1"。
    2. 如果逐份打印设置为"True"(可设置中的公共部分直接[ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构，或通过调用**SetOptions**上 **\*逐份打印**PPD 功能)，但逐份打印功能当前不可用，逐份打印将设置为"False"。
    3. 如果 **%pageorder**打印机的当前输出顺序设置相反 **%pageorder**将反转为打印机的值。

4. 仅当已启用后台处理程序 EMF 后台处理时，才支持此功能。

    如果支持，此功能设置可能会导致发生以下情况：

    1. 如果打印机的 PPD 文件包含 **\*OutputOrder**功能关键字，则将更改其选项选择以匹配的新设置的输出顺序 **%pageorder**功能。 这样做是为了防止执行不必要的页顺序模拟后台处理程序。
    2. 如果打印机的 PPD 文件不包含 **\*OutputOrder**功能和新设置用于 **%pageorder**驱动程序功能是相反的打印机的当前输出顺序设置，并 **%metafilespooling**驱动程序功能为"False"，然后 **%metafilespooling**将重置为"True"。

5. 仅当后台处理程序 EMF 后台处理，并提供了双工功能时，才支持"手册"选项。

    当支持"手册"选项，则设置 **%pagepersheet**到"手册"驱动程序功能可能会导致以下更改：

    1. 如果 **%metafilespooling**驱动程序功能为"False"，它将重置为"True"。
    2. 如果 **\*双工**PPD 功能设置为无 **\*双工**功能将重置为第一个非单纯形选项 PPD 文件中定义。

6. 中的格式指定"EPS"(内嵌的 PostScript)，除了 **%outputformat**驱动程序功能根据以下两个特征进行分类：
    1. 是输出 PostScript 代码独立于页面顺序？
    2. 没有输出 PostScript 代码包含设备控制命令 (这通常使用**setpagedevice**运算符)？

        <table>
        <colgroup>
        <col width="33%" />
        <col width="33%" />
        <col width="33%" />
        </colgroup>
        <thead>
        <tr class="header">
        <th></th>
        <th>页序独立于</th>
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
        <td><p>速度</p></td>
        <td><p>否</p></td>
        <td><p>是</p></td>
        </tr>
        </tbody>
        </table>

当**GetOptions**称为驱动程序功能关键字，如果无法识别请求的功能关键字，或如果可识别，但不是支持在当前功能关键字*文档粘滞*或*打印机粘滞*模式 (请参阅[Replacing Driver-Supplied 属性表页](replacing-driver-supplied-property-sheet-pages.md))、 功能只需将被忽略，并且输出缓冲区将包含其功能/选项关键字对。

例如，假设**GetOptions**调用方法，并*pmszFeaturesRequested*输入的缓冲区包含以下字符串 (在多\_SZ 格式):

```cpp
"Resolution\0%CustomPageSize\0Unknown_Name\0%Orientation\0\0"
```

之后**GetOption**返回时， *pmszFeatureOptionBuf*输出缓冲区可能包含此字符串 (也在多\_SZ 格式):

```cpp
"Resolution\0300dpi\0%CustomPageSize\0612 792 0 0 ShortEdge\0%Orientation\0RotatedLandscape\0\0"
```

请注意，未知\_名称的功能 （它不存在） 的第一个字符串中列出中未显示第二个字符串，因为它无法识别 Pscript 驱动程序。 其他功能，解决方法， **%custompagesize**，并 **%方向**，出现在输出字符串中，一起使用其当前的选项，这是"300 dpi"，"612 792 0 0 ShortEdge"，并"RotatedLandscape"，分别。 说明，请参阅驱动程序功能 **%custompagesize**选项。

当**SetOptions**如果请求的功能关键字或其选项关键字在输入缓冲区中的指向的驱动程序功能关键字调用*pmszFeatureOptionBuf*无法识别或功能已可识别，但不是支持在当前文档粘性或打印机粘滞模式下 (请参阅[Replacing Driver-Supplied 属性表页](replacing-driver-supplied-property-sheet-pages.md))，或功能关键字和其选项关键字识别但选项关键字对于该功能无效 (例如，尝试设置 **%ttdownloadformat**到不支持 Type42 TTRasterizer 打印机上的"NativeTrueType")，则将忽略该功能/选项对和的当前选项该功能将继续生效。

指向缓冲区中的功能/选项关键字对的顺序*pmszFeatureOptionBuf*可能会影响结果**SetOptions**调用。 例如，以下两个不同的顺序具有不同的结果。

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
<td><p>"手册"</p></td>
<td><p>"True"</p></td>
</tr>
<tr class="even">
<td><p>"%PagePerSheet\0Booklet\0%MetafileSpooling\0False\0\0"</p></td>
<td><p>"1"</p></td>
<td><p>"False"</p></td>
</tr>
</tbody>
</table>

为什么会出现这些结果的说明，请参阅备注 3 上 **%metafilespooling**、 更高版本。
