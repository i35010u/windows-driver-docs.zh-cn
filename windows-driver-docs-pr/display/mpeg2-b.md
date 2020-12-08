---
title: MPEG2_B
description: MPEG2_B
keywords:
- MPEG2_B 受限配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf959a4aef81cc016ea75fbfbb2c52a08b30ff9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799655"
---
# <a name="mpeg2_b"></a>MPEG2 \_ B


## <span id="ddk_mpeg2_b_gg"></span><span id="DDK_MPEG2_B_GG"></span>


MPEG2 \_ B 限制配置文件包含支持 mpeg-2 视频主配置文件所需的一组功能，以及使用前端缓冲区到缓冲区子画面混合的关联 DVD 子画面。 字母混合源和目标曲面的宽度和高度分别为720和576。 当前鼓励支持此配置文件，但不是必需的。

由于 [mpeg2 \_ a](mpeg2-a.md) 限制配置文件是由 mpeg2 b 配置文件的加速器要求 relaxation 定义的 \_ ，因此支持 mpeg2 b 配置文件的所有加速器都 \_ 必须支持 mpeg2 \_ A profile。

MPEG2 B 的限制 \_ 是根据 mpeg2 A 列出的限制定义的 \_ ，但以下附加限制除外。

### <a name="span-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanrestrictions-on-dxva_connectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA ConnectMode 的限制 \_

必须支持 *bDXVA \_ 函数函数* 的这些值： 1 (图片解码) ，2 (alpha 混合数据加载) ，或 3 (alpha 混合组合) 。

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
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_B</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_configalphaload_and_dxva_configalphacombinespanspan-idrestrictions_on_dxva_configalphaload_and_dxva_configalphacombinespanspan-idrestrictions_on_dxva_configalphaload_and_dxva_configalphacombinespanrestrictions-on-dxva_configalphaload-and-dxva_configalphacombine"></a><span id="Restrictions_on_DXVA_ConfigAlphaLoad_and_DXVA_ConfigAlphaCombine"></span><span id="restrictions_on_dxva_configalphaload_and_dxva_configalphacombine"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGALPHALOAD_AND_DXVA_CONFIGALPHACOMBINE"></span>DXVA \_ ConfigAlphaLoad 和 DXVA ConfigAlphaCombine 的 \_ 限制

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
<td align="left"><p><strong>bConfigBlendType</strong> (DXVA_ConfigAlphaCombine) </p></td>
<td align="left"><p>零 (前端缓冲区到缓冲区的混合) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigDataType</strong> (DXVA_ConfigAlphaLoad) </p></td>
<td align="left"><p>零个、1个或3个 (，请) </p></td>
</tr>
</tbody>
</table>

 

 

 





