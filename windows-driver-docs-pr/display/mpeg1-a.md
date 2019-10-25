---
title: MPEG1_A
description: MPEG1_A
ms.assetid: 2c4d79b7-3331-49f9-a561-6e5b609543df
keywords:
- MPEG1_A 受限配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c07300dffcc2d2840617b6b3cf626d7d61f8b530
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840547"
---
# <a name="mpeg1_a"></a>MPEG1\_


## <span id="ddk_mpeg1_a_gg"></span><span id="DDK_MPEG1_A_GG"></span>


受限制的配置文件\_MPEG1 包含支持 MPEG-2 视频所需的一组功能。 提供硬件视频加速功能的视频加速器驱动程序需要此配置文件的支持。 这组功能由以下限制集定义：

### <a name="span-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanrestrictions-on-dxva_connectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA\_ConnectMode 上的限制

当[ **\_DXVA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)的**dwFunction**成员中定义的*bDXVA\_Func*变量等于1时，适用于[**DXVA\_ConnectMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)结构的以下限制。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG1_A</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_pictureparametersspanspan-idrestrictions_on_dxva_pictureparametersspanspan-idrestrictions_on_dxva_pictureparametersspanrestrictions-on-dxva_pictureparameters"></a><span id="Restrictions_on_DXVA_PictureParameters"></span><span id="restrictions_on_dxva_pictureparameters"></span><span id="RESTRICTIONS_ON_DXVA_PICTUREPARAMETERS"></span>DXVA\_PictureParameters 上的限制

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">结构成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>BPP</em>变量（通过将1添加到<strong>bBPPminus1 定义）</strong></p></td>
<td align="left"><p>等于8</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bSecondField</strong></p></td>
<td align="left"><p>等于零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>MacroblockWidthMinus1</strong></p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>MacroblockHeightMinus1</strong></p></td>
<td align="left"><p>15</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bBlockWidthMinus1</strong></p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bBlockHeightMinus1</strong></p></td>
<td align="left"><p>7</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bChromaFormat</strong> （4:2:0）</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicStructure</strong></p></td>
<td align="left"><p>3（框架结构化）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bRcontrol</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>零（MPEG-2 双向平均）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>零（MPEG-2 半样本运动）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicExtrapolation</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicDeblocked</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPic4MVallowed</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicOBMC</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMV_RPS</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SpecificIDCT</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicScanFixed</strong></p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanspan-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanspan-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanrestrictions-on-dxva_mbctrl_i_hostresiddiff_1-dxva_mbctrl_i_offhostidct_1-dxva_mbctrl_p_hostresiddiff_1-and-dxva_mbctrl_p_offhostidct_1"></a><span id="Restrictions_on_DXVA_MBctrl_I_HostResidDiff_1__DXVA_MBctrl_I_OffHostIDCT_1__DXVA_MBctrl_P_HostResidDiff_1__and_DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="restrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1"></span><span id="RESTRICTIONS_ON_DXVA_MBCTRL_I_HOSTRESIDDIFF_1__DXVA_MBCTRL_I_OFFHOSTIDCT_1__DXVA_MBCTRL_P_HOSTRESIDDIFF_1__AND_DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>对 DXVA\_MBctrl\_I\_HostResidDiff\_1，DXVA\_MBctrl\_I\_OffHostIDCT\_1，DXVA\_MBctrl\_P\_HostResidDiff\_1和 DXVA\_MBctrl\_P\_OffHostIDCT\_1

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wMBtype 位</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>MotionType</em></p></td>
<td align="left"><p>2（帧运动）</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>MBscanMethod</em></p></td>
<td align="left"><p>如果<strong>bConfigHostInverseScan</strong>等于零，则为零（中值）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>FieldResidual</em></p></td>
<td align="left"><p>零（帧残留）</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>H261LoopFilter</em></p></td>
<td align="left"><p>零（无261循环筛选器）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_bitstream_buffersspanspan-idrestrictions_on_bitstream_buffersspanspan-idrestrictions_on_bitstream_buffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>位流缓冲区的限制

任何位流缓冲区的内容必须包含 MPEG-2 主要配置文件视频格式的数据。

 

 





