---
title: WIA\_IPA\_格式
description: WIA\_IPA\_格式属性包含要传送的图像的当前格式。 WIA 微型驱动程序创建并维护此属性。
ms.assetid: 5b60b45f-16ad-45c4-97f0-d92099f698b9
keywords:
- WIA_IPA_FORMAT 成像设备
topic_type:
- apiref
api_name:
- WIA_IPA_FORMAT
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2339edf101df144529d99b534d231159c4c950af
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369553"
---
# <a name="wiaipaformat"></a>WIA\_IPA\_格式


WIA\_IPA\_格式属性包含要传送的图像的当前格式。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_format_si"></span><span id="DDK_WIA_IPA_FORMAT_SI"></span>


属性类型：VT\_CLSID

有效值：WIA\_PROP\_列表

访问权限：读取/写入

<a name="remarks"></a>备注
-------

如果可以将设备设置一个值，创建 WIA\_PROP\_列表类型，并将有效的值放入其中。

对于 Windows 8 和更高版本的 Windows 中，已添加 WIA 的以下值\_IPA\_格式属性：

-   WiaImgFmt\_CSV

-   WiaImgFmt\_JBIG2

-   WiaImgFmt\_RawBar

-   WiaImgFmt\_RawMic

-   WiaImgFmt\_RawPat

-   WiaImgFmt\_XmlBar

-   WiaImgFmt\_XmlMic

-   WiaImgFmt\_XmlPat

从 Windows Vista 和更高版本的 Windows 开始，以下值添加为 WIA\_IPA\_格式属性：

-   WiaImgFmt\_PDFA

-   WiaImgFmt\_JBIG

-   WiaImgFmt\_XPS

有关这两个 WiaImgFmt\_PDFA 和 WiaImgFmt\_XPS 格式，驱动程序应支持任何[ **WIA\_IPA\_压缩**](wia-ipa-compression.md)值。 对于这些两个设置的格式，默认 WIA\_IPA\_压缩值，WIA\_压缩\_NONE，表示"未定义。" 扫描程序 （或驱动程序，其中生成的 PDF/A 或 XPS 文件） 必须选择用于图像数据的内部压缩模式。

下表描述了有效使用 WIA 的常量\_IPA\_格式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>格式</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WiaAudFmt_AIFF</p></td>
<td><p>AIFF 音频格式</p></td>
</tr>
<tr class="even">
<td><p>WiaAudFmt_MP3</p></td>
<td><p>MP3 音频格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaAudFmt_WAV</p></td>
<td><p>WAV 音频格式</p></td>
</tr>
<tr class="even">
<td><p>WiaAudFmt_WMA</p></td>
<td><p>WMA 音频格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_ASF</p></td>
<td><p>ASF 视频格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_AVI</p></td>
<td><p>AVI 视频格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_BMP</p></td>
<td><p>Windows 设备无关位图 (DIB) 文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_CIFF</p></td>
<td><p>照相机图像文件格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_CSV<strong></p></td>
<td><p>逗号分隔的文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_DPOF</p></td>
<td><p>DPOF 打印格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_EMF</p></td>
<td><p>扩展的 Windows 图元文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_EXEC</p></td>
<td><p>可执行文件</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_EXIF</p></td>
<td><p>可交换文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_FLASHPIX</p></td>
<td><p>FlashPix 格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_GIF</p></td>
<td><p>GIF 图像格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_HTML</p></td>
<td><p>HTML 格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_ICO</p></td>
<td><p>Windows 图标文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JBIG*</p></td>
<td><p>联合的二值图像专家组格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JBIG2</strong></p></td>
<td><p>联合二值图像专家组格式 （第 2 版）</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JPEG</p></td>
<td><p>JPEG 压缩的格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JPEG2K</p></td>
<td><p>JPEG 2000 压缩的格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JPEG2KX</p></td>
<td><p>JPEG 2000 压缩的格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_MEMORYBMP</p></td>
<td><p>Windows 位图不带标头文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_MPG</p></td>
<td><p>MPEG 视频格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PHOTOCD</p></td>
<td><p>· Kodak 文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PDFA<em></p></td>
<td><p>PDF/A (ISO/CD 19005-1) 格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PICT</p></td>
<td><p>Apple 文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_PNG</p></td>
<td><p>W3C PNG 格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RAW</p></td>
<td><p>仅数据传输的 WIA 原始图像文件格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawBar</em><em></p></td>
<td><p>WIA 条形码元数据的原始格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RawMic</em><em></p></td>
<td><p>WIA MICR 元数据的原始格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawPat</em><em></p></td>
<td><p>WIA 修补程序代码的元数据的原始格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RAWRGB</p></td>
<td><p>原始 RGB 格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RTF</p></td>
<td><p>丰富的文本文件格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_SCRIPT</p></td>
<td><p>脚本文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_TIFF</p></td>
<td><p>标记图像文件格式 (TIFF)</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_TXT</p></td>
<td><p>文本文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_UNICODE16</p></td>
<td><p>Unicode 16 位编码</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_WMF</p></td>
<td><p>Windows 图元文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XML</p></td>
<td><p>XML 文件</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_XmlBar</em><em></p></td>
<td><p>其内容是符合 WIA 条形码元数据架构的 XML 文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XmlMic</em><em></p></td>
<td><p>其内容是符合 WIA MICR 元数据架构的 XML 文件</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_XmlPat</em><em></p></td>
<td><p>其内容是符合 WIA 修补程序代码的元数据架构的 XML 文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XPS</em></p></td>
<td><p>XPS 文档文件</p></td>
</tr>
</tbody>
</table>

 

标有星号的格式 (\*) 适用于 Windows Vista 和更高版本的 Windows。

使用两个星号标记的格式 (\*\*) 适用于 Windows 8 和更高版本的 Windows。

所有 WIA 2.0 微型驱动程序必须将此属性的初始值都设置为其默认值，即 WiaImgFmt\_BMP。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h （包括 Wiadef.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA\_IPA\_压缩**](wia-ipa-compression.md)

[**WIA\_IPA\_FULL\_ITEM\_NAME**](wia-ipa-full-item-name.md)

 

 






