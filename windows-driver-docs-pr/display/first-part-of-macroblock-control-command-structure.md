---
title: 宏块控制命令结构的第一部分
description: 宏块控制命令结构的第一部分
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c53ca2feee6906b5b4340953be96eebe66d6db7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783291"
---
# <a name="first-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第一部分


## <span id="ddk_first_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FIRST_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


一般宏块控件命令结构的前四个成员始终相同。 下表描述了此结构第一部分的成员。

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
<td align="left"><p>指定当前正在处理的宏块的宏块地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wMBtype</strong></p></td>
<td align="left"><p>指定正在处理的宏块的类型。 此成员包含一些标志，该标志指示是否使用运动补偿来预测宏块的值和发送的剩余数据的类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwMB_SNL</strong></p></td>
<td align="left"><p>包含两个字段， <em>MBskipsFollowing</em> (在) 较低的8位 <em>， (在</em> 低24位) 中的。</p>
<p><em>MBskipsFollowing</em> 指定要在当前宏块之后生成的已跳过 macroblocks 的数目。</p>
<p><em>MBdataLocation</em> 是 IDCT 残留差异块数据缓冲区的索引，指示当前宏块的块的剩余差值数据的位置。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>wPatternCode</strong></p></td>
<td align="left"><p>指示是否为宏块中的每个块发送残差数据。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idwmbaddressspanspan-idwmbaddressspanspan-idwmbaddressspanwmbaddress"></a><span id="wMBaddress"></span><span id="wmbaddress"></span><span id="WMBADDRESS"></span>wMBaddress

**WMBaddress** 结构成员指定当前宏块在光栅扫描顺序中的宏块地址。 下表显示了宏块地址的示例。

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
<td align="left"><p>左上角</p></td>
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p>右上方</p></td>
<td align="left"><p><strong>wPicWidthInMBminus1</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p>左下角</p></td>
<td align="left"><p><strong>wPicHeightInMBminus1</strong> x (<strong>wPicWidthInMBminus1</strong>+ 1) </p></td>
</tr>
<tr class="even">
<td align="left"><p>右下</p></td>
<td align="left"><p> (<strong>wPicHeightInMBminus1</strong>+ 1) x (<strong>wPicWidthInMBminus1</strong>+ 1) -1</p></td>
</tr>
</tbody>
</table>

 

**WPicWidthInMBminus1** 和 **WPicHeightInMBminus1** 地址是 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的成员。

### <a name="span-idwmbtypespanspan-idwmbtypespanspan-idwmbtypespanwmbtype"></a><span id="wMBtype"></span><span id="wmbtype"></span><span id="WMBTYPE"></span>wMBtype

**WMBtype** 结构成员指定正在处理的宏块类型。 此成员包含一组定义 macroblocks 和运动向量处理方式的位。 **BPic4MVallowed**、 **bPicScanMethod**、 **bPicBackwardPrediction**、 **bPicStructure** 和 **bPicScanFixed** 地址都是 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的成员。 **BConfigHostInverseScan** 地址是 [**DXVA \_ ConfigPictureDecode**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)结构的成员。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Bits</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>15到12</p></td>
<td align="left"><p><em>MvertFieldSel_3</em> (位15，) 到 <em>MvertFieldSel</em>_0)  (</p>
<p>为稍后在宏块控件命令中发送的相应运动向量指定垂直字段选择，如下表所示。 对于带有帧图片结构的基于帧的运动 (例如，对于261和) ，这些位必须均为零。 <em>MvertFieldSel_0、MvertFieldSel_1、MvertFieldSel_2</em>和<em>MvertFieldSel_3</em>中的位对应于 mpeg-2 第6.3.17.2 部分中的 motion_vertical_field_select [r] [s] 位。</p></td>
</tr>
<tr class="even">
<td align="left"><p>11</p></td>
<td align="left"><p>保留位。 必须为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p><em>HostResidDiff</em></p>
<p>指定是否发送空间域残留差异解码块，或是否为当前宏块的脱离主机 IDCT 发送转换系数。 如果 <strong>bConfigResidDiffHost</strong> 为零，则必须为零。 如果 <strong>bConfigResidDiffAccelerator</strong> 为零，则必须为1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9和8</p></td>
<td align="left"><p><em>MotionType</em></p>
<p>指定图片中的运动类型。 例如，对于带有帧图片结构的基于帧的动画 (如 261) 中，位9必须为1，位8必须为零。</p>
<p>如果在 mpeg-2 位流中存在 MPEG-2 视频标准的6.3.17.1 和表6-17 和6-18，则使用这些位直接对应于使用该 <em>frame_motion_type</em> 或 <em>field_motion_type</em> 位。 此表后面会进一步说明这些位的使用情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>7和6</p></td>
<td align="left"><p><em>MBscanMethod</em></p>
<p>指定宏块扫描方法。 如果<strong>bPicScanFixed</strong>为1，则此必须等于<strong>bPicScanMethod</strong> 。 如果 <em>HostResidDiff</em> 为1，则此变量没有任何意义，并且应将这些位设置为零。</p>
<p>如果 <strong>bConfigHostInverseScan</strong> 为零，则 <em>MBscanMethod</em> 必须是下列值之一：</p>
<ul>
<li><p>第6位为零，而位7为零（用于中值扫描） (MPEG-2 图 7-2) </p></li>
<li><p>第6位为1，第7位为零（对于垂直扫描 7-3 (）为零) </p></li>
<li><p>第6位为零，第7位为1，适用于备用水平扫描 (.H 图 I. 2 部分 a) </p></li>
</ul>
<p>如果 <strong>bConfigHostInverseScan</strong> 为1，则 <em>MBscanMethod</em> 必须等于以下值：</p>
<ul>
<li><p>第6位为1，第7位为1，表示具有绝对系数地址的任意扫描。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p><em>FieldResidual</em></p>
<p>指示残留差异块是否使用 MPEG-2 中指定的 IDCT 结构字段。</p>
<p>如果 <strong>bPicStructure</strong> 为1或2，则此标志必须为1。 如果 MPEG-2 语法中的 <em>frame_pred_frame_DCT</em> 标志为1，则在用于 mpeg-2 时，此标志必须为零。 如果宏块存在<em>dct_type</em> ，则此标志在用于 mpeg-2 语法时必须等于 mpeg-2 语法的<em>dct_type</em>元素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p><em>H261LoopFilter</em></p>
<p>指定261循环筛选器 (节3.2.3 的 261) 对于当前宏块预测是否处于活动状态。 261循环筛选器是一种可分离的1/4、1/2、1/4 筛选器，可在水平和垂直方向上应用到261宏块中的所有六个块，只不过其中一个点击会落在块之外的块边缘除外。 在这种情况下，筛选器将更改为具有系数0，1，0。 在二维筛选器过程的输出中，将保留完全算术精度，并将其舍入到8位整数 (将) 向上舍入的半整数或更高的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p><em>Motion4MV</em></p>
<p>指示对于宏块中的四个亮度块中的每个，forward 运动都使用不同的运动向量，如在 Annexes F 和 J 中使用。如果<em>MotionForward</em>为零或<strong>bPic4MVallowed</strong>为零，则<em>Motion4MV</em>必须为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p><em>MotionBackward</em></p>
<p>此变量用于在 MPEG-2 中的相应 <em>macroblock_motion_backward</em> 参数中指定。 如果 DXVA_PictureParameters 结构的 <strong>bPicBackwardPrediction</strong> 成员为零，则 <em>MotionBackward</em> 必须为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><em>MotionForward</em></p>
<p>对于 MPEG-2 中的相应 <em>macroblock_motion_forward</em> ，将使用此变量。 此表后面的文本中进一步说明了使用此位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p><em>IntraMacroblock</em></p>
<p>指示宏块被编码为内部，并且没有用于当前宏块的运动矢量。</p>
<p>此变量对应于 MPEG-2 中的 <em>macroblock_intra</em> 变量。 此表后面的文本中进一步说明了使用此位。</p></td>
</tr>
</tbody>
</table>

 

如果 macroblocks 是预先编码的，则它们具有关联的运动矢量值。 这些值基于是否将 macroblocks 用于字段编码或框架编码图片而生成。 任何实现都应正确地考虑每个使用的宏块类型 (尤其是对于字段结构化图片或双重质数运动) 。

本部分中的以下两个表说明了 *IntraMacroblock*、 *MotionForward*、 *MotionBackward*、 *MotionType*、 *MvertFieldSel* 和 **MVector** 的有效组合。 **MVector** 包含运动向量的水平和垂直分量。 其余的变量和标志指定运动矢量运算。 这取决于处理的宏块类型，以及是否将 macroblocks 用于框架编码或字段编码图片。

此部分中 (的下表中显示的值) 在下列情况下发生：

-   *H261LoopFilter*、 *Motion4MV* 和 **bPicOBMC** 为零。

-   除非 **bPicStructure** 为 2 (底部字段) ，否则 *PicCurrentField* 标志为零。 在这种情况下， *PicCurrentField* 为1。

**MVector** 是 [**DXVA \_ MBctrl \_ p \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1) 和 [**DXVA \_ MBctrl \_ p \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1) 结构的成员。 *IntraMacroblock*、 *MotionForward*、 *MotionBackward*、 *MotionType*、 *MvertFieldSel*、 *H261LoopFilter* 和 *MOTION4MV* 标志和变量都包含在位域 **wMBtype** \_ wMBtype \_ p \_ DXVA \_ 1 和 MBctrl \_ HostResidDiff \_ p \_ DXVA \_ 1 结构的 MBctrl 成员中。 **bPicOBMC** 是 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters) 结构的成员。 *PicCurrentField* 标志派生自 DXVA PictureParameters 的 **bPicStructure** 成员 \_ 。

查看本部分中的下表时，请注意以下事项：

-   在多个位置，MPEG-2 变量名称 *PMV* 用于指示运动向量的值。 此表示法用于区分 MPEG-2 （在帧坐标中定义）中定义的 *PMV* 变量，还可以区分以半垂直分辨率) 在字段坐标 (的运动矢量。 在所有情况下， *PMV* 都是指在 (按 Mpeg-2 视频部分 7.6.3.1) 中指定的当前运动向量值更新 *后 PMV* 的值。

-   \[ \] \[ \] \[ \] \[ \] 在7.6.3.6 节中找到矢量 "2 0 和 vector" 3 0 的定义。 显示的左 **-** 移操作指示将垂直组件修改为帧坐标。

-   在 "无运动" 事例中 (0，0，0) ，宏块参数将使用零值运动向量来模拟前向预测宏块 (0，1，0) 。  (另请参阅 MPEG-2 部分7.6.3.5。 ) 

-   用单引号显示的 *MotionType* 的值为二进制表示形式， (第一个数字是第一个数字，第二个值用于位 8) 。

-   第一个表中的左移运算符仅适用于显示的第二个值。

### <a name="span-idframe-structured_picturesspanspan-idframe-structured_picturesspanspan-idframe-structured_picturesspanframe-structured-pictures"></a><span id="Frame-Structured_Pictures"></span><span id="frame-structured_pictures"></span><span id="FRAME-STRUCTURED_PICTURES"></span>框架结构化图片

下表显示了在 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicStructure** 成员等于 3) 时 (框架结构化图片的元素设置的有效组合。

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
<th align="left">MotionType (意义取决于图片类型) </th>
<th align="left">MVector [0] MvertFieldSel_0 (1，dir1) </th>
<th align="left">MVector [1] MvertFieldSel_1 (1，dir2) </th>
<th align="left">MVector [2] MvertFieldSel_2 (第二个，dir1) </th>
<th align="left">MVector [3] MvertFieldSel_3 (第二、dir2) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1，0，0 () </p></td>
<td align="left"><p>"00" (内部) </p></td>
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
<td align="left"><p>0，0，0 (无运动) </p></td>
<td align="left"><p>"10" (无运动) </p></td>
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
<td align="left"><p>0，1，0</p></td>
<td align="left"><p>"10" (帧 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，0，1</p></td>
<td align="left"><p>"10" (帧 MC) </p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>"10" (帧 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，1，0</p></td>
<td align="left"><p>"01" (字段 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，0，1</p></td>
<td align="left"><p>"01" (字段 MC) </p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="even">
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>"01" (字段 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，1，0</p></td>
<td align="left"><p>"11" (双重质数) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<div>
 
</div>
<p>0 (top) </p></td>
<td align="left"><p>vector "[2] [0] [0]，</p>
<div>
 
</div>
vector "[2] [0] [1] &lt; &lt; 1
<p>1 (底部) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<div>
 
</div>
<p>1</p></td>
<td align="left"><p>vector "[3] [0] [0]，</p>
<div>
 
</div>
vector "[3] [0] [1] &lt; &lt; 1
<p>0</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idfield-structured_picturesspanspan-idfield-structured_picturesspanspan-idfield-structured_picturesspanfield-structured-pictures"></a><span id="Field-Structured_Pictures"></span><span id="field-structured_pictures"></span><span id="FIELD-STRUCTURED_PICTURES"></span>字段结构化图片

下表显示了当 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicStructure** 成员等于1或 2) 时，字段结构化图片的元素设置的有效组合 (。

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
<th align="left">MotionType (意义取决于图片类型) </th>
<th align="left">MVector [0] MvertFieldSel_0 (1，dir1) </th>
<th align="left">MVector [1] MvertFieldSel_1 (1，dir2) </th>
<th align="left">MVector [2] MvertFieldSel_2 (第二个，dir1) </th>
<th align="left">MVector [3] MvertFieldSel_3 (第二、dir2) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1，0，0 () </p></td>
<td align="left"><p>"00" (内部) </p></td>
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
<td align="left"><p>0，0，0 (无运动) </p></td>
<td align="left"><p>"01" (无运动) </p></td>
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
<td align="left"><p>0，1，0</p></td>
<td align="left"><p>"01" (字段 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，0，1</p></td>
<td align="left"><p>"01" (字段 MC) </p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>"01" (字段 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，1，0</p></td>
<td align="left"><p>"10" (16x8 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，0，1</p></td>
<td align="left"><p>"10" (16x8 MC) </p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="even">
<td align="left"><p>0、1、1</p></td>
<td align="left"><p>"10" (16x8 MC) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p>sel [0] [0]</p></td>
<td align="left"><p>PMV [0] [1]</p>
<p>sel [0] [1]</p></td>
<td align="left"><p>PMV [1] [0]</p>
<p>sel [1] [0]</p></td>
<td align="left"><p>PMV [1] [1]</p>
<p>sel [1] [1]</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，1，0</p></td>
<td align="left"><p>"11" (双重质数) </p></td>
<td align="left"><p>PMV [0] [0]</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>vector "[2] [0]</p>
<p><em>PicCurrentField</em></p></td>
<td align="left"><p>-</p>
<p>-</p></td>
<td align="left"><p>-</p>
<p>-</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_valid_element_settings_for_field_and_frame_picturesspanspan-idadditional_valid_element_settings_for_field_and_frame_picturesspanspan-idadditional_valid_element_settings_for_field_and_frame_picturesspanadditional-valid-element-settings-for-field-and-frame-pictures"></a><span id="Additional_Valid_Element_Settings_for_Field_and_Frame_Pictures"></span><span id="additional_valid_element_settings_for_field_and_frame_pictures"></span><span id="ADDITIONAL_VALID_ELEMENT_SETTINGS_FOR_FIELD_AND_FRAME_PICTURES"></span>字段和框架图片的其他有效的元素设置

框架结构化图片和字段结构化图片的其余允许事例如下所示。

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
<td align="left"><p>指示在 <strong>MVector</strong>[0] 中发送一个向前运动向量，并且261循环筛选器对于宏块中的正向预测是活动的。</p>
<p>在这种情况下， <em>MotionForward</em>必须为1，并且<em>IntraMacroblock</em>和<em>MotionBackward</em>必须都为零。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong> = 0</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>指示在 <strong>MVector</strong>[0] 到 <strong>MVector</strong>[3] 之间发送四个前进运动向量。 在这种情况下， <em>MotionForward</em>必须为1，而<em>IntraMacroblock</em>必须为零。</p>
<p>如果 <em>MotionBackward</em> 为1，则在 <strong>MVector</strong>[4] 中发送向后预测的第五个运动向量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><em>bPicOBMC</em></strong> = 1</p>
<p><em>Motion4MV</em> = 0</p></td>
<td align="left"><p>指示将在 <strong>MVector</strong>[0] 到 <strong>MVector</strong>[9] 中发送10个前进运动向量，以指定 OBMC 动作，并且前四个运动向量的值都相等。</p>
<p>如果 <em>MotionBackward</em> 为1，则将为 <strong>MVector</strong>[10] 中的向后预测发送第11个运动矢量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>bPicOBMC</strong> = 1</p>
<p><em>Motion4MV</em> = 1</p></td>
<td align="left"><p>指示将在 <strong>MVector</strong>[0] 到 <strong>MVector</strong>[9] 中发送10个前进运动向量，以指定 OBMC 运动，并且前四个此类运动向量的值可能不同。</p>
<p>如果 <em>MotionBackward</em> 为1，则将为 <strong>MVector</strong>[10] 中的向后预测发送第11个运动矢量。</p></td>
</tr>
</tbody>
</table>

 

**注意**  Average 运算符 ( # B1 s1 + s2 + 1) &gt; &gt; 1) 用于 MPEG-2、mpeg-2 半样本预测筛选、双向平均和双质数与组合的双质数相同。 在右移位之前，H-p 双向平均运算符不会增加 + 1 的偏移量。 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的 **bBidirectionalAveragingMode** 成员确定使用哪些方法。

 

 

