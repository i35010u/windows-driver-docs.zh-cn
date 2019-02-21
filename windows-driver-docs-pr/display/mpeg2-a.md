---
title: MPEG2_A
description: MPEG2_A
ms.assetid: 4f9e2aad-4072-4a49-87df-dfc6b4bf5f56
keywords:
- MPEG2_A 受限制的配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e040c995b2796a49ce6b23c2a90003b6850b1acd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554640"
---
# <a name="mpeg2a"></a>MPEG2\_A


## <span id="ddk_mpeg2_a_gg"></span><span id="DDK_MPEG2_A_GG"></span>


MPEG2\_受限制的配置文件中包含的一组功能支持 mpeg-2 视频主配置文件所必需的。 需要提供硬件视频加速功能的视频加速器驱动程序支持此配置文件。

MPEG2\_由以下几组限制定义一个配置文件：

### <a name="span-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanspan-idrestrictionsondxvaconnectmodespanrestrictions-on-dxvaconnectmode"></a><span id="Restrictions_on_DXVA_ConnectMode"></span><span id="restrictions_on_dxva_connectmode"></span><span id="RESTRICTIONS_ON_DXVA_CONNECTMODE"></span>DXVA 限制\_ConnectMode

上的以下限制[ **DXVA\_ConnectMode** ](https://msdn.microsoft.com/library/windows/hardware/ff563138)结构时，适用*bDXVA\_Func* 中定义的变量**dwFunction**的成员[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构是否等于 1。

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

 

### <a name="span-idrestrictionsondxvapictureparametersspanspan-idrestrictionsondxvapictureparametersspanspan-idrestrictionsondxvapictureparametersspanrestrictions-on-dxvapictureparameters"></a><span id="Restrictions_on_DXVA_PictureParameters"></span><span id="restrictions_on_dxva_pictureparameters"></span><span id="RESTRICTIONS_ON_DXVA_PICTUREPARAMETERS"></span>DXVA 限制\_PictureParameters

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
<td align="left"><p><em>BPP</em>变量 (由添加到 1 定义<strong>bBPPminus1)</strong></p></td>
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
<td align="left"><p><strong>bChromaFormat</strong> (4:2:0)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bRcontrol</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>零 （mpeg-2 双向求平均值）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>零 （mpeg-2 半示例运动）</p></td>
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

 

### <a name="span-idrestrictionsondxvambctrlihostresiddiff1dxvambctrlioffhostidct1dxvambctrlphostresiddiff1anddxvambctrlpoffhostidct1spanspan-idrestrictionsondxvambctrlihostresiddiff1dxvambctrlioffhostidct1dxvambctrlphostresiddiff1anddxvambctrlpoffhostidct1spanspan-idrestrictionsondxvambctrlihostresiddiff1dxvambctrlioffhostidct1dxvambctrlphostresiddiff1anddxvambctrlpoffhostidct1spanrestrictions-on-dxvambctrlihostresiddiff1-dxvambctrlioffhostidct1-dxvambctrlphostresiddiff1-and-dxvambctrlpoffhostidct1"></a><span id="Restrictions_on_DXVA_MBctrl_I_HostResidDiff_1__DXVA_MBctrl_I_OffHostIDCT_1__DXVA_MBctrl_P_HostResidDiff_1__and_DXVA_MBctrl_P_OffHostIDCT_1"></span><span id="restrictions_on_dxva_mbctrl_i_hostresiddiff_1__dxva_mbctrl_i_offhostidct_1__dxva_mbctrl_p_hostresiddiff_1__and_dxva_mbctrl_p_offhostidct_1"></span><span id="RESTRICTIONS_ON_DXVA_MBCTRL_I_HOSTRESIDDIFF_1__DXVA_MBCTRL_I_OFFHOSTIDCT_1__DXVA_MBCTRL_P_HOSTRESIDDIFF_1__AND_DXVA_MBCTRL_P_OFFHOSTIDCT_1"></span>限制 DXVA\_MBctrl\_我\_HostResidDiff\_月 1 日，DXVA\_MBctrl\_我\_OffHostIDCT\_1，DXVA\_MBctrl\_P\_HostResidDiff\_1 和 DXVA\_MBctrl\_P\_OffHostIDCT\_1

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">wMBtype Bits</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>MBscanMethod</em></p></td>
<td align="left"><p>可能是零 （z 形） 的值或值为 1 （备用垂直） 如果<strong>ConfigHostInverseScan</strong>的成员<a href="https://msdn.microsoft.com/library/windows/hardware/ff563133" data-raw-source="[&lt;strong&gt;DXVA_ConfigPictureDecode&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563133)"> <strong>DXVA_ConfigPictureDecode</strong> </a>等于零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>H261LoopFilter</p></td>
<td align="left"><p>零</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>位流缓冲区的限制

任何位流缓冲区的内容必须包含 mpeg-2 主配置文件的视频格式的数据。

**BNewQmatrix**的成员[ **DXVA\_QmatrixData** ](https://msdn.microsoft.com/library/windows/hardware/ff564034)为等于零，我使用反转量化矩阵时 = 2 和 3。

 

 





