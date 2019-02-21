---
title: MPEG2_B
description: MPEG2_B
ms.assetid: 7d67f0ef-a5eb-40db-9f00-6f652d28e530
keywords:
- MPEG2_B 受限制的配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3980f104c81fb3d6e3fa88987e0574428700a6d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548135"
---
# <a name="mpeg2b"></a>MPEG2\_B


## <span id="ddk_mpeg2_b_gg"></span><span id="DDK_MPEG2_B_GG"></span>


MPEG2\_B 受限制的配置文件中包含的一组功能所需的 mpeg-2 视频主配置文件和使用前端缓冲区缓冲区子画面值混合处理关联的 DVD 子画面的支持。 分别使用宽度和高度至少 720 和 576，支持 alpha 值混合处理源和目标图面。 此配置文件的支持目前建议使用，但不是必需的。

因为[MPEG2\_A](mpeg2-a.md) MPEG2 的加速器要求是放宽了由定义受限制的配置文件\_B 配置文件、 所有加速器支持 MPEG2\_B 配置文件必须支持MPEG2\_一个配置文件。

MPEG2 的限制\_MPEG2 为列出的限制由定义 B\_A，但下面的其他限制除外。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA 限制\_ConnectMode

这些值的*bDXVA\_Func*必须支持变量：（图解码） 的 1、 2 （正在加载 alpha 混合数据） 或 3 （alpha 混合组合）。

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
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_B</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigalphaloadanddxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphaloadanddxvaconfigalphacombinespanspan-idrestrictionsondxvaconfigalphaloadanddxvaconfigalphacombinespanrestrictions-on-dxvaconfigalphaload-and-dxvaconfigalphacombine"></a><span id="Restrictions_on_DXVA_ConfigAlphaLoad_and_DXVA_ConfigAlphaCombine"></span><span id="restrictions_on_dxva_configalphaload_and_dxva_configalphacombine"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHALOAD_AND_DXVA_CONFIGALPHACOMBINE"></span>限制 DXVA\_ConfigAlphaLoad 和 DXVA\_ConfigAlphaCombine

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
<td align="left"><p><strong>bConfigBlendType</strong> (DXVA_ConfigAlphaCombine)</p></td>
<td align="left"><p>零 （前端缓冲区缓冲区值混合处理）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigDataType</strong> (DXVA_ConfigAlphaLoad)</p></td>
<td align="left"><p>0，1 或 3 (快捷键在&#39;s 自行决定)</p></td>
</tr>
</tbody>
</table>

 

 

 





