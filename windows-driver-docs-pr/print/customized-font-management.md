---
title: 自定义的字体管理
description: 自定义的字体管理
ms.assetid: 6e643703-ace1-4660-990c-3a9ca735829d
keywords:
- Unidrv，字体
- 字体管理 WDK Unidrv
- 自定义字体管理 WDK Unidrv
- ufm 文件
- UFM 文件
- gtt 文件
- GTT 文件
- uff 文件
- UFF 文件
- 设备字体 WDK Unidrv
- 字体盒式 WDK Unidrv
- 可下载的 PCL 软字体 WDK Unidrv
- PCL 软字体 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53ecde093b173c6b0833bc4c5929cf478359a0ae
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242882"
---
# <a name="customized-font-management"></a>自定义的字体管理





对于*PCL*打印机，Unidrv 支持将软字体下载为位图或 TrueType 轮廓。 对于设备字体，Unidrv 支持 PCL、CAPSL 和 PPDS 打印机命令格式。 对于其他格式，必须在呈现插件中提供自定义的字体管理代码。 可以实现以下 IPrintOemUni 方法集：

<a href="" id="iprintoemuni--downloadfontheader"></a>[**IPrintOemUni：:D ownloadFontHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadfontheader)  
用于从 Unidrv 获取软字体的标头信息，然后将信息下载到打印机。

<a href="" id="iprintoemuni--downloadcharglyph"></a>[**IPrintOemUni：:D ownloadCharGlyph**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-downloadcharglyph)  
用于将软字体的字符标志符号下载到打印机。

<a href="" id="iprintoemuni--outputcharstr"></a>[**IPrintOemUni::OutputCharStr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-outputcharstr)  
用于控制字符打印。

<a href="" id="iprintoemuni--sendfontcmd"></a>[**IPrintOemUni::SendFontCmd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-sendfontcmd)  
用于修改打印机的设备字体选择命令，并在必要时将其发送到打印机。

<a href="" id="iprintoemuni--textoutasbitmap"></a>[**IPrintOemUni::TextOutAsBitmap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)  
用于创建文本字符串的位图图像。

<a href="" id="iprintoemuni--ttdownloadmethod"></a>[**IPrintOemUni::TTDownloadMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-ttdownloadmethod)  
用于指定 Unidrv 在向打印机发送指定软字体时应使用的标志符号格式。

Unidrv 提供回调函数[*UNIFONTOBJ\_GetInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/nc-printoem-pfngetinfo)，呈现插件可以调用来获取字体或字形信息。

对于设备字体，必须按 " **Unidrv font 公制 files** " 一节中所述提供字体说明，并提供 "**字形转换表文件**" 部分。

对于字体盒字体，可在资源 Dll 中提供字体说明，并使用字体盒文件指定。 还可以以 Unidrv 字体格式文件的形式提供字体说明。

对于可下载的 PCL 软字体，必须提供字体说明，如**Unidrv 字体格式文件**部分所述。

### <a href="" id="ddk-unidrv-font-metrics-files-gg"></a>Unidrv 字体指标文件

打印机支持的每个设备字体必须由 Unidrv 字体指标（. ufm）文件表示。 Ufm 文件是二进制文件，使用[Unidrv 字体度量结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)中所述的结构构造。 Ufm 文件中的第一个结构是[**UNIFM\_HDR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_unifm_hdr)，其中包含文件其他结构的偏移量。 下图显示了 Unidrv 字体指标文件的布局。

![说明 unidrv 字体指标文件布局的关系图](images/ufm.png)

Unidrv 还支持 ifi 文件，这是为 Windows NT 4.0 创建的字体指标文件。

### <a href="" id="ddk-glyph-translation-table-files-gg"></a>字形转换表文件

打印机支持的每个设备字体必须由一个字形转换表（. gtt）文件表示。 Gtt 文件是二进制文件，使用[Unidrv 字形转换表结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)中所述的结构构造。 Gtt 文件中的第一个结构是包含文件其他结构的偏移量的[**单向\_GLYPHSETDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uni_glyphsetdata)结构。

下图显示了字形转换表文件的布局。

![说明字形转换表文件布局的关系图](images/gtt.png)

在上图中，单向\_GLYPHSETDATA 结构包含从文件开头到第一个[**GLYPHRUN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_glyphrun)结构的偏移量、第一个[**单向\_CODEPAGEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uni_codepageinfo)结构和[**MAPTABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_maptable)结构。

Unidrv 还支持为 Windows NT 4.0 创建的字形转换文件，该文件使用运行长度编码（RLE）压缩并且具有 RLE 扩展名。

### <a href="" id="ddk-unidrv-font-format-files-gg"></a>Unidrv 字体格式文件

对于未使用字体盒软字体指定的字体盒字体，必须使用 uff 文件指定。

Uff 文件是使用以下结构集构造的二进制文件：

-   [Unidrv 字体格式结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)，用于定义 uff 文件的内容和结构。

-   [Unidrv font 度量结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)，用于定义每个字体的指标。

-   [Unidrv 字形转换表结构](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)，用于定义字体使用的字形集。

下图显示了 Unidrv 字体格式文件的布局。

![说明 unidrv 字体格式文件的布局的关系图](images/uff.png)

Unidrv 字体格式文件由[**UFF\_FILEHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uff_fileheader)结构和一个或多个[**UFF\_FONTDIRECTORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_uff_fontdirectory)和[**数据\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prntfont/ns-prntfont-_data_header)结构对组成。 每个数据\_标头结构与一个字体数据块关联。 UFF\_FILEHEADER 结构包含从文件开头到第一个 UFF\_FONTDIRECTORY 结构的偏移量。 每个 UFF\_FONTDRECTORY 结构都包含从文件开始到包含字体数据的数据\_标头结构的偏移量。

此外，对于可下载的*PCL*软字体，要下载的二进制数据存储在 uff 文件中。

uff 文件创建由供应商提供的字体安装软件负责。 Unidrv 读取打印机的 uff 文件以获取字体和字形信息。 添加或删除字体时，字体安装程序应修改 uff 文件的内容。 有关创建字体安装程序的详细信息，请参阅[Unidrv 的自定义字体安装](customized-font-installers-for-unidrv.md)程序。

所有 uff 文件必须存储在% SystemRoot%\\System32\\线轴\\驱动程序\\Unifont 目录中。 若要将单独的 uff 文件与特定打印机关联，安装软件必须调用 SetPrinterData 函数（如 Windows SDK 文档中所述），以便在每个打印机的注册表项下创建注册表值。 下表列出了必须使用的注册表值名称，并指示每个值的 maintainer。

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
<th>员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>"ExternalFontFile"</p>
<p>REG_SZ</p></td>
<td><p>Uff 文件的文件名，该文件指定当前安装的字体。 字体可以是可下载的，也可以包含在盒式磁带中。</p></td>
<td><p>字体安装程序</p></td>
</tr>
<tr class="even">
<td><p>"ExtFontCartFile"</p>
<p>REG_SZ</p></td>
<td><p>Uff 文件的文件名，该文件指定为 "ExtFontCartNames" 列出的所有字体盒中包含的所有字体。</p></td>
<td><p>字体安装程序</p></td>
</tr>
<tr class="odd">
<td><p>"ExtFontCartNames"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>可能在打印机上安装的所有字体盒的名称。</p></td>
<td><p>字体安装程序</p></td>
</tr>
<tr class="even">
<td><p>"FontCart"</p>
<p>REG_MULTI_SZ</p></td>
<td><p>当前为打印机安装的所有字体盒的名称。</p></td>
<td><p>Unidrv 用户界面</p></td>
</tr>
</tbody>
</table>

 

将字体盒添加到打印机后，系统管理员必须运行字体安装程序，该安装程序负责将字体说明从 "ExtFontCartFile" 指定的 uff 文件复制到 "ExternalFontFile" 指定的 uff 文件中。 同样，在删除磁带时，字体安装程序必须从 "ExtFontCartFile" 指定的 uff 文件中删除字体说明。

 

 




