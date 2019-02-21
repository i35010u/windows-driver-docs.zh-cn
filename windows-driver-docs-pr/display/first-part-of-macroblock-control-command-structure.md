---
title: 第一部分宏块控制命令结构
description: 第一部分宏块控制命令结构
ms.assetid: b282adac-3bf3-4477-a817-371d37b174a5
keywords:
- 宏块 WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad4893102e2bcbc00046ee9d2c2064fe13e20d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544669"
---
# <a name="first-part-of-macroblock-control-command-structure"></a>第一部分宏块控制命令结构


## <span id="ddk_first_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FIRST_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


泛型宏块控制命令结构的前四个成员始终是相同的。 下表描述此结构的第一个部分的成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>wMBaddress</strong></p></td>
<td align="left"><p>指定当前正在处理宏块的宏块地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wMBtype</strong></p></td>
<td align="left"><p>指定的宏块正在处理的类型。 此成员包含这些标志指示是否使用运动补偿来预测宏块的值以及发送什么类型的残留的差异数据。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwMB_SNL</strong></p></td>
<td align="left"><p>包含两个字段<em>MBskipsFollowing</em> （在上的 8 位） 和<em>MBdataLocation</em> （以较低的 24 位）。</p>
<p><em>MBskipsFollowing</em>指定已跳过宏块为其生成以下当前宏块的数目。</p>
<p><em>MBdataLocation</em>是 IDCT 残留差异块数据缓冲区，指示当前宏块的块的残留的差异数据的位置的索引。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wPatternCode</strong></p></td>
<td align="left"><p>指示是否为宏块中的每个块发送残留不同的数据。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idwmbaddressspanspan-idwmbaddressspanspan-idwmbaddressspanwmbaddress"></a><span id="wMBaddress"></span><span id="wmbaddress"></span><span id="WMBADDRESS"></span>wMBaddress

**WMBaddress**结构成员指定当前宏块的宏块地址光栅扫描顺序。 下表显示了宏块地址的示例。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏块</th>
<th align="left">地址</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>top-left</p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p>top-right</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>lower-left</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong>+ 1)</p></td>
</tr>
<tr class="even">
<td align="left"><p>lower-right</p></td>
<td align="left"><p>(<strong>wPicHeightInMBminus1</strong>+ 1) x (<strong>wPicWidthInMBminus1</strong>+ 1)-1</p></td>
</tr>
</tbody>
</table>

 

**WPicWidthInMBminus1**并**wPicHeightInMBminus1**地址属于[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。

### <a name="span-idwmbtypespanspan-idwmbtypespanspan-idwmbtypespanwmbtype"></a><span id="wMBtype"></span><span id="wmbtype"></span><span id="WMBTYPE"></span>wMBtype

**WMBtype**结构成员指定宏块正在处理的类型。 此成员包含一组位的定义方式宏块和动作矢量进行处理。 **BPic4MVallowed**， **bPicScanMethod**， **bPicBackwardPrediction**， **bPicStructure**，和**bPicScanFixed**地址属于[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。 **BConfigHostInverseScan**地址属于[ **DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>15 到 12</p></td>
<td align="left"><p><em>MvertFieldSel_3</em> （15，最高有效位） 通过<em>MvertFieldSel</em>_0 （12 位）</p>
<p>指定垂直字段选定内容的更高版本在宏块控制命令中，指定下表中发送的相应动作矢量。 基于框架的动作与帧图片结构 （例如，对于 H.261 和 H.263），这些位必须全部为零。 中的位<em>MvertFieldSel_0、 MvertFieldSel_1、 MvertFieldSel_2，</em>并<em>MvertFieldSel_3</em>对应于 motion_vertical_field_select [r] [s] 位的 mpeg-2 6.3.17.2 部分中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>保留的位。 必须为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p><em>HostResidDiff</em></p>
<p>指定是否发送空间域残留差异解码块，或是否为当前宏块的非主机 IDCT 发送转换系数。 必须为零<strong>bConfigResidDiffHost</strong>为零。 必须为 1，如果<strong>bConfigResidDiffAccelerator</strong>为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9 和 8</p></td>
<td align="left"><p><em>MotionType</em></p>
<p>图中指定的动作类型。 例如，基于框架的动作与帧图片结构 （如同一 H.261)，9 位必须为 1，位 8 必须为零。</p>
<p>使用这些位对应于使用直接<em>frame_motion_type</em>或<em>field_motion_type</em>部分 6.3.17.1 和表 6-17 和 mpeg-2 视频标准，这些位时的 6-18 中位MPEG 2 位流中存在。 使用这些位将进一步说明此表后面。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7 和 6</p></td>
<td align="left"><p><em>MBscanMethod</em></p>
<p>指定的宏块扫描方法。 这必须等于<strong>bPicScanMethod</strong>如果<strong>bPicScanFixed</strong>为 1。 如果<em>HostResidDiff</em>为 1，此变量没有任何意义，应将这些位设置为零。</p>
<p>如果<strong>bConfigHostInverseScan</strong>为零， <em>MBscanMethod</em>必须是以下值之一：</p>
<ul>
<li><p>第 6 位为 0，7 位为零的上上下下的锯齿形扫描 (mpeg-2 图 7-2)</p></li>
<li><p>6 位是 1 和 7 位为零的备用垂直扫描 (mpeg-2 图 7-3)</p></li>
<li><p>第 6 位为 0，7 位为 1 表示备用水平扫描 (H.263 图 I.2 部分)</p></li>
</ul>
<p>如果<strong>bConfigHostInverseScan</strong>为 1， <em>MBscanMethod</em>必须等于以下值：</p>
<ul>
<li><p>第 6 位为 1，7 位是 1 表示任意扫描具有绝对系数地址。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p><em>FieldResidual</em></p>
<p>指示是否残留差异块使用字段 IDCT 结构 MPEG 2 中指定。</p>
<p>此标志必须为 1，如果<strong>bPicStructure</strong>为 1 或 2。 此标志必须为零，如果使用 mpeg-2 <em>frame_pred_frame_DCT</em> mpeg-2 语法中的标记为 1。 此标志必须为等于<em>dct_type</em> mpeg-2 语法时使用 mpeg-2 如果元素<em>dct_type</em>存在可用于宏块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><em>H261LoopFilter</em></p>
<p>指定是否 H.261 循环筛选器 （3.2.3 节的 H.261） 处于活动状态的当前宏块预测。 H.261 循环筛选器是可分离 ¼、 ½、 ¼ 应用于筛选器同时水平和垂直 H.261 宏块中中的所有六个块除外块的两端的两次点击一个将落入块外部。 在这种情况下，更改筛选器具有系数 0，1，0。 舍入为 8 位整数的二维筛选器进程 （半整数或更高版本的值被向上舍入） 的输出将保留完整算术精度。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><em>Motion4MV</em></p>
<p>指示向前移动宏块中的四个亮度基块的每个使用不同的动作矢量用作 H.263 附录 F 和 J. <em>Motion4MV</em>必须为零<em>MotionForward</em>为零或者如果<strong>bPic4MVallowed</strong>为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><em>MotionBackward</em></p>
<p>使用此变量指定相应<em>macroblock_motion_backward</em> MPEG 2 中的参数。 如果<strong>bPicBackwardPrediction</strong> DXVA_PictureParameters 结构中的成员为零， <em>MotionBackward</em>必须为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><em>MotionForward</em></p>
<p>使用此变量指定相应<em>macroblock_motion_forward</em> MPEG 2 中。 在此表后面的文本，进一步介绍了使用此位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p><em>IntraMacroblock</em></p>
<p>指示宏块被编码为内部并没有动作矢量可用于当前宏块。</p>
<p>此变量对应于<em>macroblock_intra</em> MPEG 2 中用户定义变量。 在此表后面的文本，进一步介绍了使用此位。</p></td>
</tr>
</tbody>
</table>

 

当预先编码块效应时，它们具有关联的动作矢量值。 基于块效应用于字段编码或编码帧的图片所生成的值。 非常重要的任何实现来正确应对每个已利用的宏块类型 （尤其是对于结构字段的图片或双素数运动）。

在本部分中的以下两个表表示的有效组合*IntraMacroblock*， *MotionForward*， *MotionBackward*， *MotionType*， *MvertFieldSel*，和**MVector**帧编码和字段编码图片。 **MVector**包含动作矢量的水平和垂直组件。 剩余的变量和标志指定动作矢量运算。 这决定根据宏块处理的类型和宏块正在使用框架编码或字段编码图片。

（在本部分中） 下面的表中所示的值出现在以下条件：

-   *H261LoopFilter*， *Motion4MV*，和**bPicOBMC**均为零。

-   *PicCurrentField*标志为零，除非**bPicStructure**为 2 （底部字段）。 在这种情况下， *PicCurrentField*为 1。

**MVector**隶属[ **DXVA\_MBctrl\_P\_HostResidDiff\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563993)和[ **DXVA\_MBctrl\_P\_OffHostIDCT\_1** ](https://msdn.microsoft.com/library/windows/hardware/ff563997)结构。 *IntraMacroblock*， *MotionForward*， *MotionBackward*， *MotionType*， *MvertFieldSel*， *H261LoopFilter*，并*Motion4MV*标志和变量是位域中包含**wMBtype** DXVA 成员\_MBctrl\_P\_HostResidDiff\_1 和 DXVA\_MBctrl\_P\_OffHostIDCT\_1 结构。 **bPicOBMC**隶属[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构。 *PicCurrentField*标志派生自**bPicStructure** DXVA 成员\_PictureParameters。

阅读此部分中的以下表时，应考虑以下事项：

-   中的许多位置、 MPEG 2 变量名*PMV*用于指示动作矢量的值。 此表示法用于区分*PMV* MPEG 2 中定义变量，后者位于帧坐标，并可能在字段坐标 （换而言之，在后半部分垂直分辨率） 的动作矢量。 在所有情况下， *PMV*的值是指*PMV 后的*已更新当前的动作矢量值 （作为中的指定 mpeg-2 视频部分 7.6.3.1)。

-   向量的定义\[2\]\[0\]和向量\[3\]\[0\] mpeg-2 一节中找到 7.6.3.6。 左侧**-** 移位运算所示，则表示的垂直分量修改为帧坐标。

-   在这两种情况下，"不传输"(0,0,0)，宏块参数模拟具有零值动作矢量的正向预测宏块 (0,1,0)。 （请参阅 mpeg-2 部分 7.6.3.5。）

-   显示值*MotionType*用单引号将二进制表示形式 （第一个数字是 9 位的第二项是为 8 位）。

-   第一个表中的左移运算符仅适用于显示的第二个值。

### <a name="span-idframe-structuredpicturesspanspan-idframe-structuredpicturesspanspan-idframe-structuredpicturesspanframe-structured-pictures"></a><span id="Frame-Structured_Pictures"></span><span id="frame-structured_pictures"></span><span id="FRAME-STRUCTURED_PICTURES"></span>结构帧的图片

下表显示了框架结构化图片的元素设置的有效组合 (当**bPicStructure**的成员[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构是否等于 3)。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IntraMacroblock, MotionForward, MotionBackward</th>
<th align="left">MotionType （含义取决于图片类型）</th>
<th align="left">MVector[0]MvertFieldSel_0 (1st, dir1)</th>
<th align="left">MVector[1]MvertFieldSel_1 (1st, dir2)</th>
<th align="left">MVector[2]MvertFieldSel_2 (2nd, dir1)</th>
<th align="left">MVector[3]MvertFieldSel_3 (2nd, dir2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1,0,0 （内部）</p></td>
<td align="left"><p>&#39;00&#39; （内部）</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,0 （不移动）</p></td>
<td align="left"><p>&#39;10&#39; （不移动）</p></td>
<td align="left"><p>0</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>&#39;10&#39; （帧 MC）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>&#39;10&#39; （帧 MC）</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>&#39;10&#39; （帧 MC）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>-</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>&#39;01&#39; （字段 MC）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>sel[0][0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[1][0]</p>
<p>sel[1][0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>&#39;01&#39; （字段 MC）</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>sel[0][1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[1][1]</p>
<p>sel[1][1]</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>&#39;01&#39; （字段 MC）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>sel[0][0]</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>sel[0][1]</p></td>
<td align="left"><p>PMV[1][0]</p>
<p>sel[1][0]</p></td>
<td align="left"><p>PMV[1][1]</p>
<p>sel[1][1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>&#39;11&#39; （双质数）</p></td>
<td align="left"><p>PMV[0][0]</p>
<div>
 
</div>
<p>0 （上图）</p></td>
<td align="left"><p>vector&#39;[2][0][0],</p>
<div>
 
</div>
vector&#39;[2][0][1]&lt;&lt;1
<p>1 （下图）</p></td>
<td align="left"><p>PMV[0][0]</p>
<div>
 
</div>
<p>1</p></td>
<td align="left"><p>vector&#39;[3][0][0],</p>
<div>
 
</div>
vector&#39;[3][0][1]&lt;&lt;1
<p>0</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfield-structuredpicturesspanspan-idfield-structuredpicturesspanspan-idfield-structuredpicturesspanfield-structured-pictures"></a><span id="Field-Structured_Pictures"></span><span id="field-structured_pictures"></span><span id="FIELD-STRUCTURED_PICTURES"></span>结构字段的图片

下表显示了结构字段的图片的元素设置的有效组合 (当**bPicStructure**的成员[ **DXVA\_PictureParameters**](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构是否等于 1 或 2)。

<table>
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">IntraMacroblock, MotionForward, MotionBackward</th>
<th align="left">MotionType （含义取决于图片类型）</th>
<th align="left">MVector[0]MvertFieldSel_0 (1st, dir1)</th>
<th align="left">MVector[1]MvertFieldSel_1 (1st, dir2)</th>
<th align="left">MVector[2]MvertFieldSel_2 (2nd, dir1)</th>
<th align="left">MVector[3]MvertFieldSel_3(2nd, dir2)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1,0,0 （内部）</p></td>
<td align="left"><p>&#39;00&#39; （内部）</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,0 （不移动）</p></td>
<td align="left"><p>&#39;01&#39; （不移动）</p></td>
<td align="left"><p>0</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>&#39;01&#39; （字段 MC）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>sel[0][0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>&#39;01&#39; （字段 MC）</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>sel[0][1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>&#39;01&#39; （字段 MC）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>sel[0][0]</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>sel[0][1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>&#39;10&#39; (16x8 MC)</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>sel[0][0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[1][0]</p>
<p>sel[1][0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,0,1</p></td>
<td align="left"><p>&#39;10&#39; (16x8 MC)</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>sel[0][1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV[1][1]</p>
<p>sel[1][1]</p></td>
</tr>
<tr class="even">
<td align="left"><p>0,1,1</p></td>
<td align="left"><p>&#39;10&#39; (16x8 MC)</p></td>
<td align="left"><p>PMV[0][0]</p>
<p>sel[0][0]</p></td>
<td align="left"><p>PMV[0][1]</p>
<p>sel[0][1]</p></td>
<td align="left"><p>PMV[1][0]</p>
<p>sel[1][0]</p></td>
<td align="left"><p>PMV[1][1]</p>
<p>sel[1][1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0,1,0</p></td>
<td align="left"><p>&#39;11&#39; （双质数）</p></td>
<td align="left"><p>PMV[0][0]</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>vector&#39;[2][0]</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalvalidelementsettingsforfieldandframepicturesspanspan-idadditionalvalidelementsettingsforfieldandframepicturesspanspan-idadditionalvalidelementsettingsforfieldandframepicturesspanadditional-valid-element-settings-for-field-and-frame-pictures"></a><span id="Additional_Valid_Element_Settings_for_Field_and_Frame_Pictures"></span><span id="additional_valid_element_settings_for_field_and_frame_pictures"></span><span id="ADDITIONAL_VALID_ELEMENT_SETTINGS_FOR_FIELD_AND_FRAME_PICTURES"></span>字段和帧图片的其他有效的元素设置

帧结构化和结构字段的图片的其余允许的事例如下所示。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>H261LoopFilter</em> = 1</p>
<p><strong>bPicOBMC</strong> = 0</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>指示发送一个进动作矢量<strong>MVector</strong>[0] 和 H.261 循环筛选器处于活动状态正预测宏块中。</p>
<p><em>MotionForward</em>这种情况下，必须为 1 并且<em>IntraMacroblock</em>并<em>MotionBackward</em>必须都为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong> = 0</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>指示发送的四个进动作矢量<strong>MVector</strong>[0] 通过<strong>MVector</strong>[3]。 <em>MotionForward</em>这种情况下，必须为 1 并且<em>IntraMacroblock</em>必须为零。</p>
<p>如果<em>MotionBackward</em>为 1，第五个动作矢量发送中的向后预测<strong>MVector</strong>[4]。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>bPicOBMC</em></strong> = 1</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>指示以发送 10 进动作矢量<strong>MVector</strong>[0] 通过<strong>MVector</strong>[9] 对于 OBMC 规范运动、 和的前四个此类值动作矢量是均相等。</p>
<p>如果<em>MotionBackward</em>为 1，第 11 个动作矢量发送中的向后预测<strong>MVector</strong>[10]。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong> = 1</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>指示以发送 10 进动作矢量<strong>MVector</strong>[0] 通过<strong>MVector</strong>[9] OBMC 规范的运动，和的前四个此类值动作矢量可能不同于每个其他。</p>
<p>如果<em>MotionBackward</em>为 1，第 11 个动作矢量发送中的向后预测<strong>MVector</strong>[10]。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  平均运算符是数学上完全相同 ((s1 + s2 + 1)&gt;&gt;1) 对于 MPEG-1，mpeg-2 半示例预测筛选、 双向求平均值和双素数相同相反奇偶校验组合. H.263 双向平均运算符不会添加之前右移位 + 1 的偏移量。 **BBidirectionalAveragingMode**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)确定哪种方法使用。

 

 

 





