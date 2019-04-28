---
title: MPEG2_C
description: MPEG2_C
ms.assetid: 610ca80d-b29a-4c30-98df-8df8fe825157
keywords:
- MPEG2_C 受限制的配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efdd51cc9e0cc8fec615e36c1dce9534acac1b4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345649"
---
# <a name="mpeg2c"></a>MPEG2\_C


## <span id="ddk_mpeg2_c_gg"></span><span id="DDK_MPEG2_C_GG"></span>


MPEG2\_C 受限制的配置文件中包含的一组功能支持 mpeg-2 视频主配置文件所必需的。 需要提供硬件视频加速功能的视频加速器驱动程序支持此配置文件。

因为 MPEG2\_C 受限制的配置文件定义的加速器要求是放宽了由[MPEG2\_A](mpeg2-a.md) （通过允许加速器为不支持的最小成员中的任何配置文件互操作性为 MPEG2\_A)，所有加速器支持 MPEG2\_配置文件必须支持 MPEG2\_C 配置文件。 同样，支持的所有快捷键[MPEG2\_D](mpeg2-d.md)配置文件必须支持 MPEG2\_C 配置文件。

限制的 MPEC2\_MPEG2 为列出的限制由定义 C\_A，但下面的其他限制除外。

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA 限制\_ConnectMode

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
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_C</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanspan-idrestrictionsondxvaconfigpicturedecodespanrestrictions-on-dxvaconfigpicturedecode"></a><span id="Restrictions_on_DXVA_ConfigPictureDecode"></span><span id="restrictions_on_dxva_configpicturedecode"></span><span id="RESTRICTIONS_ON_DXVA_CONFIGPICTUREDECODE"></span>DXVA 限制\_ConfigPictureDecode

此配置文件将添加到配置的其他[最小互操作性集](minimal-interoperability-configuration-sets.md)用于解码图片。 此附加配置由以下 DXVA\_ConfigPictureDecode 成员。

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
<td align="left"><p><strong>bConfigResidDiffHost</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bConfigResidDiffAccelerator</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

 

 





