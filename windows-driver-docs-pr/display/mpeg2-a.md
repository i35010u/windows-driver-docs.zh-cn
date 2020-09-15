---
title: MPEG2_A
description: MPEG2_A
ms.assetid: 4f9e2aad-4072-4a49-87df-dfc6b4bf5f56
keywords:
- MPEG2_A 受限配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4ae101a74bbc611fc6681ef986dedde833487bd
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90106566"
---
# <a name="mpeg2_a"></a>MPEG2 \_ A


## <span id="ddk_mpeg2_a_gg"></span><span id="DDK_MPEG2_A_GG"></span>


\_限制配置文件包含支持 mpeg-2 视频主配置文件所需的一组功能。 提供硬件视频加速功能的视频加速器驱动程序需要此配置文件的支持。

MPEG2 \_ ：配置文件由下列限制集定义：

### <a name="span-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanspan-idrestrictions_on_dxva_connectmodespanrestrictions-on-dxva_connectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA ConnectMode 的限制 \_

当[**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的**dwFunction**成员中定义的*bDXVA \_ Func*变量等于1时，适用于[**DXVA \_ ConnectMode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_connectmode)结构的以下限制。

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
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG2_A</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_pictureparametersspanspan-idrestrictions_on_dxva_pictureparametersspanspan-idrestrictions_on_dxva_pictureparametersspanrestrictions-on-dxva_pictureparameters"></a><span id="Restrictions_on_DXVA_PictureParameters"></span><span id="restrictions_on_dxva_pictureparameters"></span><span id="RESTRICTIONS_ON_DXVA_PICTUREPARAMETERS"></span>DXVA PictureParameters 的限制 \_

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
<td align="left"><p>0x0A</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>BPP</em>变量 (通过将1添加到<strong>bBPPminus1</strong>来定义) </p></td>
<td align="left"><p>8</p></td>
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
<td align="left"><p><strong>bChromaFormat</strong> (4:2:0) </p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bRcontrol</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>零 (MPEG-2 双向平均) </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>零 (MPEG-2 半采样动作) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicExtrapolation</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicDeblocked</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPic4MVallowed</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bMV_RPS</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>SpecificIDCT</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicScanFixed</strong></p></td>
<td align="left"><p>1</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanspan-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanspan-idrestrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1spanrestrictions-on-dxva_mbctrl_i_hostresiddiff_1-dxva_mbctrl_i_offhostidct_1-dxva_mbctrl_p_hostresiddiff_1-and-dxva_mbctrl_p_offhostidct_1"></a><span id="Restrictions_on_DXVA_MBctrl_I_HostResidDiff_1__DXVA_MBctrl_I_OffHostIDCT_1__DXVA_MBctrl_P_HostResidDiff_1__and_DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="restrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1"></span><span id="RESTRICTIONS_ON_DXVA_MBCTRL_I_HOSTRESIDDIFF_1__DXVA_MBCTRL_I_OFFHOSTIDCT_1__DXVA_MBCTRL_P_HOSTRESIDDIFF_1__AND_DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>DXVA \_ MBctrl \_ i \_ HOSTRESIDDIFF \_ 1、DXVA \_ MBCTRL \_ i \_ OffHostIDCT \_ 1、DXVA \_ MBctrl \_ p \_ HostResidDiff \_ 1 和 DXVA \_ MBctrl \_ p \_ OffHostIDCT \_ 1 的限制

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wMBtype 位</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>MBscanMethod</em></p></td>
<td align="left"><p>如果<a href="/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode" data-raw-source="[&lt;strong&gt;DXVA_ConfigPictureDecode&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)"><strong>DXVA_ConfigPictureDecode</strong></a>的<strong>ConfigHostInverseScan</strong>成员等于零，则值可以为零 (之字形) 或值 1 (备用垂直) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>H261LoopFilter</p></td>
<td align="left"><p>零</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictions_on_bitstream_buffersspanspan-idrestrictions_on_bitstream_buffersspanspan-idrestrictions_on_bitstream_buffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>位流缓冲区的限制

任何位流缓冲区的内容必须包含 MPEG-2 主要配置文件视频格式的数据。

使用反量化矩阵时， [**DXVA \_ QmatrixData**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_qmatrixdata)的**bNewQmatrix**成员等于零，i = 2 和3。

