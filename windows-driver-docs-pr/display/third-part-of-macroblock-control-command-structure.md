---
title: 宏块控制命令结构的第三部分
description: 宏块控制命令结构的第三部分
ms.assetid: 4e378d2f-dbb2-42b6-984e-b231bb806a7c
keywords:
- macroblocks WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01ec5135818ad45cd5d7707299f76a3673e3a07f
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063772"
---
# <a name="third-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第三部分


## <span id="ddk_third_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_THIRD_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


如果[**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bPicIntra**成员为1，则宏块 Control 命令结构以[宏块 Control 命令结构的第二部分](second-part-of-macroblock-control-command-structure.md)所述的数据结尾。 如果 **bPicIntra** 为零，则宏块控件命令中将包含以下附加数据元素，以控制运动补偿过程。 下面的数据是 [**DXVA \_ MVvalue**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mvvalue) 结构的数组，其中包含在宏块控件命令结构的 **MVector** 成员中。 **MVector**中的元素数取决于 \_ 下表中 DXVA PictureParameters 成员指定的图片类型。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bPicOBMC</th>
<th align="left">bPicBinPB</th>
<th align="left">bPic4MVallowed</th>
<th align="left">MVector 中的元素数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>4</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>5</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>10</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>11</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>11</p></td>
</tr>
</tbody>
</table>

 

**注意**   在**MVector**数组中为*dxva*文件中定义的宏块控制命令结构指定的运动矢量数量为四，因为这是最常用的结构形式。

 

 

