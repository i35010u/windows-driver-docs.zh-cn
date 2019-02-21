---
title: PTP 格式代码映射到 WIA 格式 Guid
description: PTP 格式代码映射到 WIA 格式 Guid
ms.assetid: a69269c0-1474-4de5-9a08-94902ef1f089
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e19dcb705575aa728b4a167379795247c4b9aa6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525195"
---
# <a name="mapping-ptp-format-codes-to-wia-format-guids"></a>PTP 格式代码映射到 WIA 格式 Guid





通过公开一个对象的格式[ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)以 GUID 形式表示的属性。 PTP 格式代码和 WIA Guid 之间的映射表所示：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>PTP 设置代码格式</th>
<th>对象类型</th>
<th>WIA GUID</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x3000</p></td>
<td><p>未定义</p></td>
<td><p>不适用。</p></td>
</tr>
<tr class="even">
<td><p>0x3001</p></td>
<td><p>关联</p></td>
<td><p>请参阅<a href="mapping-ptp-associations-to-wia-folders.md" data-raw-source="[Mapping PTP Associations to WIA Folders](mapping-ptp-associations-to-wia-folders.md)">将 PTP 关联映射到 WIA 文件夹</a>。</p></td>
</tr>
<tr class="odd">
<td><p>0x3002</p></td>
<td><p>脚本</p></td>
<td><p>DATAFMT_SCRIPT</p></td>
</tr>
<tr class="even">
<td><p>0x3003</p></td>
<td><p>可执行文件</p></td>
<td><p>DATAFMT_EXEC</p></td>
</tr>
<tr class="odd">
<td><p>0x3004</p></td>
<td><p>文本</p></td>
<td><p>DATAFMT_UNICODE16</p></td>
</tr>
<tr class="even">
<td><p>0x3005</p></td>
<td><p>HTML</p></td>
<td><p>DATAFMT_HTML</p></td>
</tr>
<tr class="odd">
<td><p>0x3006</p></td>
<td><p>DPOF</p></td>
<td><p>DATAFMT_DPOF</p></td>
</tr>
<tr class="even">
<td><p>0x3007</p></td>
<td><p>AIFF</p></td>
<td><p>AUDFMT_AIFF</p></td>
</tr>
<tr class="odd">
<td><p>0x3008</p></td>
<td><p>WAV</p></td>
<td><p>AUDFMT_WAV</p></td>
</tr>
<tr class="even">
<td><p>0x3009</p></td>
<td><p>MP3</p></td>
<td><p>AUDFMT_MP3</p></td>
</tr>
<tr class="odd">
<td><p>0x300A</p></td>
<td><p>AVI</p></td>
<td><p>VIDFMT_AVI</p></td>
</tr>
<tr class="even">
<td><p>0x300B</p></td>
<td><p>MPEG</p></td>
<td><p>VIDFMT_MPEG</p></td>
</tr>
<tr class="odd">
<td><p>0x300C</p></td>
<td><p>ASF</p></td>
<td><p>VIDFMT_ASF</p></td>
</tr>
<tr class="even">
<td><p>0x3800</p></td>
<td><p>未定义的图像</p></td>
<td><p>不适用。</p></td>
</tr>
<tr class="odd">
<td><p>0x3801</p></td>
<td><p>EXIF/JPEG</p></td>
<td><p>WiaImgFmt_JPEG</p></td>
</tr>
<tr class="even">
<td><p>0x3802</p></td>
<td><p>TIFF/EP</p></td>
<td><p>WiaImgFmt_TIFF</p></td>
</tr>
<tr class="odd">
<td><p>0x3803</p></td>
<td><p>FlashPix</p></td>
<td><p>WiaImgFmt_FLASHPIX</p></td>
</tr>
<tr class="even">
<td><p>0x3804</p></td>
<td><p>BMP</p></td>
<td><p>WiaImgFmt_BMP</p></td>
</tr>
<tr class="odd">
<td><p>0x3805</p></td>
<td><p>CIFF</p></td>
<td><p>WiaImgFmt_CIFF</p></td>
</tr>
<tr class="even">
<td><p>0x3806</p></td>
<td><p>未定义的 （保留）</p></td>
<td><p>不适用。</p></td>
</tr>
<tr class="odd">
<td><p>0x3807</p></td>
<td><p>GIF</p></td>
<td><p>WiaImgFmt_GIF</p></td>
</tr>
<tr class="even">
<td><p>0x3808</p></td>
<td><p>JFIF</p></td>
<td><p>WiaImgFmt_JPEG</p></td>
</tr>
<tr class="odd">
<td><p>0x3809</p></td>
<td><p>PCD (PhotoCD 映像 Pac)</p></td>
<td><p>WiaImgFmt_PHOTOCD</p></td>
</tr>
<tr class="even">
<td><p>0x380A</p></td>
<td><p>PICT</p></td>
<td><p>WiaImgFmt_PICT</p></td>
</tr>
<tr class="odd">
<td><p>0x380B</p></td>
<td><p>PNG</p></td>
<td><p>WiaImgFmt_PNG</p></td>
</tr>
<tr class="even">
<td><p>0x380C</p></td>
<td><p>未定义的 （保留）</p></td>
<td><p>不适用。</p></td>
</tr>
<tr class="odd">
<td><p>0x380D</p></td>
<td><p>TIFF</p></td>
<td><p>WiaImgFmt_TIFF</p></td>
</tr>
<tr class="even">
<td><p>0x380E</p></td>
<td><p>TIFF / 它</p></td>
<td><p>WiaImgFmt_TIFF</p></td>
</tr>
<tr class="odd">
<td><p>0x380F</p></td>
<td><p>JPEG2000 Baseline</p></td>
<td><p>WiaImgFmt_JPEG2K</p></td>
</tr>
<tr class="even">
<td><p>0x3810</p></td>
<td><p>JPEG2000 扩展</p></td>
<td><p>WiaImgFmt_JPEG2KX</p></td>
</tr>
</tbody>
</table>

 

(WiaImgFmt\_中定义 XXX Guid *wiadef.h*。)

 

 




