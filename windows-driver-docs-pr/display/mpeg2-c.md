---
title: MPEG2_C
description: MPEG2_C
keywords:
- MPEG2_C 受限配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48acd57975cd256aad511e5c6ee519755dcd300e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799653"
---
# <a name="mpeg2_c"></a>MPEG2 \_ C


## <span id="ddk_mpeg2_c_gg"></span><span id="DDK_MPEG2_C_GG"></span>


MPEG2 \_ C 限制配置文件包含支持 mpeg-2 视频主配置文件所需的一组功能。 提供硬件视频加速功能的视频加速器驱动程序需要此配置文件的支持。

由于 MPEG2 \_ c 限制配置文件是由 [mpeg2 \_ a](mpeg2-a.md) profile (的加速器要求的 relaxation 定义的，因此，如果允许加速器不支持 mpeg2 a) 的最小互操作集的任何成员 \_ ，则支持配置文件的所有加速器 \_ 必须支持 mpeg2 \_ C 配置文件。 同样，支持 [mpeg2 \_ D](mpeg2-d.md) 配置文件的所有加速器都必须支持 mpeg2 \_ C 配置文件。

MPEC2 C 的限制 \_ 由 MPEG2 A 列出的限制定义 \_ ，但以下附加限制除外。

### <a name="span-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanrestrictions-on-dxva_connectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA ConnectMode 的限制 \_

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_C</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_configpicturedecodespanspan-idrestrictions_on_dxva_configpicturedecodespanspan-idrestrictions_on_dxva_configpicturedecodespanrestrictions-on-dxva_configpicturedecode"></a><span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>DXVA ConfigPictureDecode 的限制 \_

此配置文件将其他配置添加到 [最小互操作集](minimal-interoperability-configuration-sets.md) 以便进行图片解码。 此附加配置由以下 DXVA \_ ConfigPictureDecode 成员定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





