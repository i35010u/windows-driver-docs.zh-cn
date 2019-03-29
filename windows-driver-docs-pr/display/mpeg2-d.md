---
title: MPEG2_D
description: MPEG2_D
ms.assetid: f5cb5e49-c64c-46d2-92bb-68db1d9c5d18
keywords:
- MPEG2_D 受限制的配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54578361f7883c035bf97bab3e315fe4ccfd0d25
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349208"
---
# <a name="mpeg2d"></a>MPEG2\_D


## <span id="ddk_mpeg2_d_gg"></span><span id="DDK_MPEG2_D_GG"></span>


MPEG2\_D 受限制的配置文件中包含的一组功能所需的 mpeg-2 视频主配置文件和使用后端硬件子画面值混合处理关联的 DVD 子画面的支持。

因为 MPEG2\_D 受限制的配置文件定义的加速器要求是放宽了由[MPEG2\_B](mpeg2-b.md) （加速器不支持需要最小互操作性设置的配置文件有关 MPEG2\_B)，所有驱动程序的支持 MPEG2\_B 配置文件必须支持 MPEG2\_D 配置文件。 MPEG2 的限制\_MPEG2 为列出的限制由定义 D\_B 受限制的配置文件，但下面的其他限制除外。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA 限制\_ConnectMode

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_D</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanrestrictions-on-dxvaconfigpicturedecode"></a><span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>DXVA 限制\_ConfigPictureDecode

这些限制将添加到配置的其他[最小互操作性集](minimal-interoperability-configuration-sets.md)用于解码图片 (bDXVA\_Func 等于 1)。 此附加配置由以下 DXVA\_ConfigPictureDecode 成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">值</th>
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

 

### <a name="span-idrestrictionsondxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphacombinespanrestrictions-on-dxvaconfigalphacombine"></a><span id="Restrictions_on_DXVA_ConfigAlphaCombine"></span><span id="restrictions_on_dxva_configalphacombine"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHACOMBINE"></span>DXVA 限制\_ConfigAlphaCombine

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigBlendType</strong></p></td>
<td align="left"><p>零个或 1 （在加速器的自行决定）。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigalphaloadspanspan-idrestrictionsondxvaconfigalphaloadspanspan-idrestrictionsondxvaconfigalphaloadspanrestrictions-on-dxvaconfigalphaload"></a><span id="Restrictions_on_DXVA_ConfigAlphaLoad"></span><span id="restrictions_on_dxva_configalphaload"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHALOAD"></span>DXVA 限制\_ConfigAlphaLoad

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>bConfigDataType</strong></p></td>
<td align="left"><p>（在加速器的自行决定） 的任何值。</p></td>
</tr>
</tbody>
</table>

 

 

 





