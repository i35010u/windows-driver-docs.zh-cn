---
title: MPEG1_A
description: MPEG1_A
ms.assetid: 2c4d79b7-3331-49f9-a561-6e5b609543df
keywords:
- MPEG1_A 受限制的配置文件 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f230f191c6b5383192f4366dab6940670ef9babd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345643"
---
# <a name="mpeg1a"></a>MPEG1\_A


## <span id="ddk_mpeg1_a_gg"></span><span id="DDK_MPEG1_A_GG"></span>


MPEG1\_受限制的配置文件中包含的一组支持 mpeg-1 视频所需的功能。 需要提供硬件视频加速功能的视频加速器驱动程序支持此配置文件。 这组功能由以下一组限制定义：

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
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wRestrictedMode</strong></p></td>
<td align="left"><p>DXVA_RESTRICTED_MODE_MPEG1_A</p></td>
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
<td align="left"><p><em>BPP</em>变量 (由添加到 1 定义<strong>bBPPminus1)</strong></p></td>
<td align="left"><p>等于 8</p></td>
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
<td align="left"><p><strong>bChromaFormat</strong> (4:2:0)</p></td>
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicStructure</strong></p></td>
<td align="left"><p>3 （结构化的帧）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bRcontrol</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bBidirectionalAveragingMode</strong></p></td>
<td align="left"><p>零 （mpeg-2 双向求平均值）</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bMVprecisionAndChromaRelation</strong></p></td>
<td align="left"><p>零 （mpeg-2 半示例运动）</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicExtrapolation</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicDeblocked</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPic4MVallowed</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>bPicOBMC</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bMV_RPS</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>SpecificIDCT</strong></p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicScanFixed</strong></p></td>
<td align="left"><p>零</p></td>
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
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>MotionType</em></p></td>
<td align="left"><p>2 （帧运动）</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>MBscanMethod</em></p></td>
<td align="left"><p>零 （z 形） if <strong>bConfigHostInverseScan</strong>等于零</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>FieldResidual</em></p></td>
<td align="left"><p>零 （帧残差）</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>H261LoopFilter</em></p></td>
<td align="left"><p>零 （无 H.261 循环筛选器）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanspan-idrestrictionsonbitstreambuffersspanrestrictions-on-bitstream-buffers"></a><span id="Restrictions_on_Bitstream_Buffers"></span><span id="restrictions_on_bitstream_buffers"></span><span id="RESTRICTIONS_ON_BITSTREAM_BUFFERS"></span>位流缓冲区的限制

任何位流缓冲区的内容必须包含 mpeg-1 主配置文件的视频格式的数据。

 

 





