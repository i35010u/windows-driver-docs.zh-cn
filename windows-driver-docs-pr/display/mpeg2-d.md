---
title: MPEG2_D
description: MPEG2_D
keywords:
- MPEG2_D 受限配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fbbe9fe08eb88ea7c1060b06957b51dfad3a3d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799651"
---
# <a name="mpeg2_d"></a>MPEG2 \_ D


## <span id="ddk_mpeg2_d_gg"></span><span id="DDK_MPEG2_D_GG"></span>


MPEG2 \_ D 限制配置文件包含支持 mpeg-2 视频主配置文件所需的一组功能，以及使用后端硬件子画面混合的关联 DVD 子画面。

由于 MPEG2 \_ d 限制配置文件是由 [mpeg2 \_ b](mpeg2-b.md) 配置文件的加速器要求 relaxation 定义的 (因此，不需要加速器 b) 支持最低互操作性集 \_ ，所有支持 mpeg2 b 配置文件的驱动程序都 \_ 必须支持 mpeg2 \_ D 配置文件。 MPEG2 D 的限制 \_ 由 mpeg2 \_ B 限制配置文件中列出的限制定义，但以下附加限制除外。

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
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_D</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_configpicturedecodespanspan-idrestrictions_on_dxva_configpicturedecodespanspan-idrestrictions_on_dxva_configpicturedecodespanrestrictions-on-dxva_configpicturedecode"></a><span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>DXVA ConfigPictureDecode 的限制 \_

这些限制将额外的配置添加到 [最小互操作集](minimal-interoperability-configuration-sets.md) ，以进行图片解码 (bDXVA \_ Func 等于 1) 。 此附加配置由以下 DXVA \_ ConfigPictureDecode 成员定义。

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

 

### <a name="span-idrestrictions_on_dxva_configalphacombinespanspan-idrestrictions_on_dxva_configalphacombinespanspan-idrestrictions_on_dxva_configalphacombinespanrestrictions-on-dxva_configalphacombine"></a><span id="Restrictions_on_DXVA_ConfigAlphaCombine"></span><span id="restrictions_on_dxva_configalphacombine"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHACOMBINE"></span>DXVA ConfigAlphaCombine 的限制 \_

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
<td align="left"><p><strong>bConfigBlendType</strong></p></td>
<td align="left"><p>0或 1 (在加速器的) 。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_configalphaloadspanspan-idrestrictions_on_dxva_configalphaloadspanspan-idrestrictions_on_dxva_configalphaloadspanrestrictions-on-dxva_configalphaload"></a><span id="Restrictions_on_DXVA_ConfigAlphaLoad"></span><span id="restrictions_on_dxva_configalphaload"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHALOAD"></span>DXVA ConfigAlphaLoad 的限制 \_

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
<td align="left"><p><strong>bConfigDataType</strong></p></td>
<td align="left"><p> (在加速器的决定) 的任何值。</p></td>
</tr>
</tbody>
</table>

 

 

 





