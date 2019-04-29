---
title: 自定义的字体管理
description: 自定义的字体管理
ms.assetid: 6e643703-ace1-4660-990c-3a9ca735829d
keywords:
- Unidrv 字体
- 字体管理 WDK Unidrv
- 自定义的字体管理 WDK Unidrv
- .ufm 文件
- UFM 文件
- .gtt 文件
- GTT 文件
- .uff 文件
- UFF 文件
- 设备字体 WDK Unidrv
- 插件字体 WDK Unidrv
- 可下载 PCL 软字体 WDK Unidrv
- PCL 软字体 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0316bf0a365cf18eb7e7cbf2a68afc73712c36d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365589"
---
# <a name="customized-font-management"></a>自定义的字体管理





有关*PCL*打印机，Unidrv 支持下载软字体当作位图或 TrueType 概述了。 为设备字体 Unidrv 支持 PCL，CAPSL，和 PPDS 打印机命令格式。 对于其他格式，必须在插件呈现提供自定义的字体管理代码。 可以实现以下组 IPrintOemUni 方法：

<a href="" id="iprintoemuni--downloadfontheader"></a>[**IPrintOemUni::DownloadFontHeader**](https://msdn.microsoft.com/library/windows/hardware/ff554242)  
用于从 Unidrv 获取软字体的标头信息，然后下载到打印机的信息。

<a href="" id="iprintoemuni--downloadcharglyph"></a>[**IPrintOemUni::DownloadCharGlyph**](https://msdn.microsoft.com/library/windows/hardware/ff554241)  
用于下载到打印机的软字体的字符标志符号。

<a href="" id="iprintoemuni--outputcharstr"></a>[**IPrintOemUni::OutputCharStr**](https://msdn.microsoft.com/library/windows/hardware/ff554267)  
用于控制打印的字符。

<a href="" id="iprintoemuni--sendfontcmd"></a>[**IPrintOemUni::SendFontCmd**](https://msdn.microsoft.com/library/windows/hardware/ff554274)  
用于修改打印机的设备字体选择命令，如有必要，可将其发送到打印机。

<a href="" id="iprintoemuni--textoutasbitmap"></a>[**IPrintOemUni::TextOutAsBitmap**](https://msdn.microsoft.com/library/windows/hardware/ff554277)  
用于创建位图图像的文本字符串。

<a href="" id="iprintoemuni--ttdownloadmethod"></a>[**IPrintOemUni::TTDownloadMethod**](https://msdn.microsoft.com/library/windows/hardware/ff554279)  
用于指定它将指定的软字体发送到打印机时，应使用 Unidrv 的标志符号格式。

Unidrv 提供一个回调函数， [ *UNIFONTOBJ\_GetInfo*](https://msdn.microsoft.com/library/windows/hardware/ff563594)，呈现插件可调用以获取字体或标志符号的信息。

对于设备字体字体说明必须具有如中所述的提供**Unidrv 字体指标文件**部分以及**标志符号转换表文件**部分。

插件字体说明可以在资源 Dll 中提供和使用字体墨盒文件指定。 字体描述也可以在 Unidrv 字体格式文件的形式提供。

对于可下载 PCL 软字体字体说明必须具有如中所述的提供**Unidrv 字体格式文件**部分。

### <a href="" id="ddk-unidrv-font-metrics-files-gg"></a>Unidrv 字体指标文件

必须由 Unidrv 字体规格 (.ufm) 文件表示打印机支持每个设备字体。 .Ufm 文件是使用中所述的结构构造的二进制文件[Unidrv 字体指标结构](https://msdn.microsoft.com/library/windows/hardware/ff563547)。 .Ufm 文件中的第一个结构[ **UNIFM\_HDR**](https://msdn.microsoft.com/library/windows/hardware/ff563587)，其中包含的文件偏移量的其他结构。 下图显示了 Unidrv 字体规格文件的布局。

![说明 unidrv 字体指标文件布局的关系图](images/ufm.png)

Unidrv 还支持.ifi 文件，为 Windows NT 4.0 创建字体指标文件。

### <a href="" id="ddk-glyph-translation-table-files-gg"></a>标志符号转换表文件

必须由标志符号转换表 (.gtt) 文件表示打印机支持每个设备字体。 .Gtt 文件是使用中所述的结构构造的二进制文件[Unidrv 标志符号转换表结构](https://msdn.microsoft.com/library/windows/hardware/ff563549)。 .Gtt 文件中的第一个结构[ **UNI\_GLYPHSETDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff563597)结构，其中包含的文件偏移量的其他结构。

下图显示标志符号转换表文件的布局。

![说明的标志符号转换表文件布局的关系图](images/gtt.png)

在上图中，单元\_GLYPHSETDATA 结构包含与第一个从文件开头的偏移量[ **GLYPHRUN** ](https://msdn.microsoft.com/library/windows/hardware/ff550544)结构，与第一个[ **UNI\_CODEPAGEINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff563596)结构，并对其[ **MAPTABLE** ](https://msdn.microsoft.com/library/windows/hardware/ff556509)结构。

Unidrv 还支持标志符号转换为创建的文件 Windows NT 4.0，它使用运行长度编码 (RLE) 压缩并具有.rle 扩展名。

### <a href="" id="ddk-unidrv-font-format-files-gg"></a>Unidrv 字体格式文件

对于未指定使用字体盒的墨盒字体以软字体都必须使用.uff 文件指定。

.Uff 文件是使用以下结构的集构造一个二进制文件：

-   [Unidrv 字体格式结构](https://msdn.microsoft.com/library/windows/hardware/ff562892)，用于定义应用程序的内容和.uff 文件的结构。

-   [Unidrv 字体指标结构](https://msdn.microsoft.com/library/windows/hardware/ff563547)，用于定义应用程序的每种字体的度量值。

-   [Unidrv 标志符号转换表结构](https://msdn.microsoft.com/library/windows/hardware/ff563549)，用于定义应用程序使用的字体的标志符号集。

下图显示了 Unidrv 字体格式文件的布局。

![说明 unidrv 字体格式文件布局的关系图](images/uff.png)

Unidrv 字体格式文件组成[ **UFF\_FILEHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff562862)结构，以及一个或多个[ **UFF\_FONTDIRECTORY**](https://msdn.microsoft.com/library/windows/hardware/ff562866)并[**数据\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff547364)结构对。 每个数据\_标头结构是字体数据块与相关联。 UFF\_FILEHEADER 结构包含从文件开头的偏移量，到第一个 UFF\_FONTDIRECTORY 结构。 每个 UFF\_FONTDRECTORY 结构包含的数据从文件开头的偏移量\_标头结构，其中包含字体数据。

此外，对于可下载*PCL*软字体，要下载的二进制数据存储在.uff 文件。

.uff 文件创建负责的供应商提供的字体安装软件。 Unidrv 读取打印机的.uff 文件以获取字体和字形信息。 添加或删除字体时，字体安装程序应修改.uff 文件内容。 有关创建字体安装程序的详细信息，请参阅[Unidrv 为自定义字体安装程序](customized-font-installers-for-unidrv.md)。

所有.uff 文件必须都存储在 %systemroot%\\System32\\Spool\\驱动程序\\Unifont 目录。 若要将单个.uff 文件与特定打印机相关联，安装软件必须调用 SetPrinterData 函数 （Windows SDK 文档中所述） 来创建每个打印机的注册表项下的注册表值。 下表列出了必须使用，并指示每个值的 maintainer 的注册表值名称。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表值名称和类型</th>
<th>值定义</th>
<th>Maintainer</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"ExternalFontFile"</p>
<p>REG_SZ</p></td>
<td><p>指定当前已安装的字体的.uff 文件的文件名。 字体可以是可下载或包含在一个磁带中。</p></td>
<td><p>字体安装程序</p></td>
</tr>
<tr class="even">
<td><p>"ExtFontCartFile"</p>
<p>REG_SZ</p></td>
<td><p>指定为"ExtFontCartNames"列出的所有字体盒中包含的所有字体.uff 文件的文件名。</p></td>
<td><p>字体安装程序</p></td>
</tr>
<tr class="odd">
<td><p>"ExtFontCartNames"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>可能无法安装在打印机的所有字体墨盒的名称。</p></td>
<td><p>字体安装程序</p></td>
</tr>
<tr class="even">
<td><p>"FontCart"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>当前为打印机安装的所有字体墨盒的名称。</p></td>
<td><p>Unidrv 用户界面</p></td>
</tr>
</tbody>
</table>

 

添加对打印机的字体插件后，系统管理员必须运行字体安装程序中，这是需要复制到指定的"ExternalFontFile".uff 文件指定的"ExtFontCartFile".uff 文件中的字体说明。 同样，字体安装程序必须从"ExtFontCartFile"删除磁带时指定的.uff 文件删除字体说明。

 

 




