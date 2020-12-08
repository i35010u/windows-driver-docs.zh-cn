---
title: WIA \_ IPA \_ 格式
description: WIA \_ IPA \_ format 属性包含即将传输的图像的当前格式。 WIA 微型驱动程序创建并维护此属性。
keywords:
- WIA_IPA_FORMAT 图像设备
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
ms.openlocfilehash: b5f699d5a68bf4ca9ed05d6f14ae7df059bb72de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817307"
---
# <a name="wia_ipa_format"></a>WIA \_ IPA \_ 格式


WIA \_ IPA \_ format 属性包含即将传输的图像的当前格式。 WIA 微型驱动程序创建并维护此属性。

## <span id="ddk_wia_ipa_format_si"></span><span id="DDK_WIA_IPA_FORMAT_SI"></span>


属性类型： VT \_ CLSID

有效值： WIA 内容 \_ \_ 列表

访问权限：读/写

<a name="remarks"></a>备注
-------

如果可以将设备设置为仅使用单个值，请创建一个 "WIA" \_ \_ 类型的 "类型"，并在其中放置有效值。

对于 Windows 8 及更高版本的 Windows，为 WIA \_ IPA FORMAT 属性添加了以下值 \_ ：

-   WiaImgFmt \_ CSV

-   WiaImgFmt \_ JBIG2

-   WiaImgFmt \_ RawBar

-   WiaImgFmt \_ RawMic

-   WiaImgFmt \_ RawPat

-   WiaImgFmt \_ XmlBar

-   WiaImgFmt \_ XmlMic

-   WiaImgFmt \_ XmlPat

从 Windows Vista 和更高版本的 Windows 开始，为 WIA \_ IPA FORMAT 属性添加了以下值 \_ ：

-   WiaImgFmt \_ PDFA

-   WiaImgFmt \_ JBIG

-   WiaImgFmt \_ XPS

对于 WiaImgFmt \_ PDFA 和 WiaImgFmt \_ XPS 格式，驱动程序应支持任何 [**WIA \_ IPA \_ 压缩**](wia-ipa-compression.md) 值。 对于这两种格式，默认的 WIA \_ IPA \_ 压缩值 "wia \_ 压缩无" \_ 表示 "未定义"。 扫描仪 (或驱动程序（在其中生成 PDF/A 或 XPS 文件）) 必须选择用于图像数据的内部压缩模式。

下表描述了对 WIA IPA 格式有效的常量 \_ \_ 。

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
<td><p>.AIFF 音频格式</p></td>
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
<td><p>与 Windows 设备无关的位图 (DIB) 文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_CIFF</p></td>
<td><p>相机图像文件格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_CSV<strong></p></td>
<td><p>逗号分隔文件</p></td>
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
<td><p>WiaImgFmt_JBIG *</p></td>
<td><p>联合 Bi 级别映像专家组格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JBIG2</strong></p></td>
<td><p>联合 Bi 级别映像专家组格式 (版本 2) </p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JPEG</p></td>
<td><p>JPEG 压缩格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_JPEG2K</p></td>
<td><p>JPEG 2000 压缩格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_JPEG2KX</p></td>
<td><p>JPEG 2000 压缩格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_MEMORYBMP</p></td>
<td><p>不带标头文件的 Windows 位图</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_MPG</p></td>
<td><p>MPEG 视频格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_PHOTOCD</p></td>
<td><p>Eastman Kodak 文件格式</p></td>
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
<td><p>WIA Raw 映像文件格式仅用于数据传输</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawBar</em><em></p></td>
<td><p>WIA 条码元数据原始格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RawMic</em><em></p></td>
<td><p>WIA 磁墨元数据原始格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RawPat</em><em></p></td>
<td><p>WIA 修补程序代码元数据原始格式</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_RAWRGB</p></td>
<td><p>原始 RGB 格式</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_RTF</p></td>
<td><p>Rtf 文件格式</p></td>
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
<td><p>其内容符合 WIA 条码元数据架构的 XML 文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XmlMic</em><em></p></td>
<td><p>其内容符合 WIA 磁墨元数据架构的 XML 文件</p></td>
</tr>
<tr class="odd">
<td><p>WiaImgFmt_XmlPat</em><em></p></td>
<td><p>其内容符合 WIA 修补程序代码元数据架构的 XML 文件</p></td>
</tr>
<tr class="even">
<td><p>WiaImgFmt_XPS</em></p></td>
<td><p>XPS 文档文件</p></td>
</tr>
</tbody>
</table>

 

用星号标记 () 的格式 \* 仅适用于 Windows Vista 和更高版本的 windows。

\* \* 仅适用于 windows 8 和更高版本的 windows () 用两个星号标记的格式。

所有 WIA 2.0 微型驱动程序都必须将此属性的初始值设置为其默认值（即 WiaImgFmt） \_ 。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WIA \_ IPA \_ 压缩**](wia-ipa-compression.md)

[**WIA \_ IPA \_ 完整 \_ 项 \_ 名称**](wia-ipa-full-item-name.md)

 

 






